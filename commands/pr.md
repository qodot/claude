---
allowed-tools: Bash(git:*), Bash(gh:*), Read(*), Grep(*)
description: 현재 브랜치를 푸시하고 GitHub PR을 작성합니다
argument-hint: [--no-draft] [--base=<브랜치>]
---

# Claude Command: pr

## 사용법
```
/pr [--no-draft] [--base=<브랜치>]

옵션:
  --no-draft: 일반 PR로 생성 (기본값: draft)
  --base: 베이스 브랜치 지정 (기본값: main)
```

## 이 명령어가 하는 일
현재 Git 브랜치의 변경사항을 분석하고, 원격 저장소에 푸시한 후, 프로젝트 규칙에 맞는 GitHub Pull Request를 자동으로 생성합니다. Django 프로젝트의 PR 템플릿과 네이밍 규칙을 준수하며, 변경사항을 의미있게 요약하여 리뷰어가 이해하기 쉬운 PR을 작성합니다.

## 역할 정의
당신은 Git 워크플로우와 GitHub 협업 도구의 전문가입니다. Django 백엔드 프로젝트의 구조와 규칙을 깊이 이해하고 있으며, 효과적인 PR 작성과 코드 리뷰 프로세스에 정통합니다. 변경사항의 맥락을 파악하고 기술적 세부사항을 명확하게 전달하는 능력을 갖추고 있습니다.

## 프로세스

### 1단계: 현재 상태 파악 및 plan.yml 확인

**병렬로 다음 정보를 수집합니다:**

1. **Git 정보 수집**
   - 현재 브랜치 이름 확인 및 형식 검증
   - git status로 스테이징되지 않은 변경사항 확인
   - git diff로 전체 변경 내용 파악
   - git log로 최근 커밋 히스토리 확인
   - 원격 브랜치와의 동기화 상태 확인

2. **plan.yml 확인 (선택적)**
   ```bash
   # 현재 브랜치 이름 추출
   BRANCH=$(git rev-parse --abbrev-ref HEAD)

   # plan.yml 경로 확인
   PLAN_FILE=".claude/features/${BRANCH}/plan.yml"
   ```

   - `.claude/features/<브랜치명>/plan.yml` 파일 존재 여부 확인
   - 있으면: plan.yml 읽기 및 파싱
   - 없으면: 기존 방식대로 git log 분석 진행

   **plan.yml이 있는 경우:**
   ```
   ✅ plan.yml 발견!

   /feature 명령어로 생성된 계획을 활용하여 PR을 생성합니다.
   - PR 제목: <plan.yml의 pr_info.title>
   - 배경 정보: <plan.yml의 background>
   - 변경 내용: <plan.yml의 changes>
   - 테스트 계획: <plan.yml의 testing>
   ```

   **plan.yml이 없는 경우:**
   ```
   ℹ️  plan.yml을 찾을 수 없습니다.

   커밋 히스토리를 분석하여 PR을 생성합니다.
   ```

### 2단계: 브랜치 정보 분석
- 브랜치 이름에서 SPR 티켓 번호 추출 (예: SPR-3040)
- 브랜치 이름이 규칙을 따르지 않으면 사용자에게 경고
- 베이스 브랜치와의 차이점 분석 (git diff main...HEAD)

### 3단계: 변경사항 분류
변경사항을 다음과 같이 분류합니다:
- **기능 추가**: 새로운 API 엔드포인트, 모델, 서비스
- **버그 수정**: 오류 수정, 예외 처리 개선
- **리팩토링**: 코드 구조 개선, 성능 최적화
- **테스트**: 테스트 코드 추가 또는 수정
- **문서화**: 문서 업데이트, 주석 추가

### 4단계: 브랜치 푸시
```bash
git push -u origin <현재-브랜치>
```
- 첫 푸시인 경우 -u 플래그로 업스트림 설정
- 이미 푸시된 경우 강제 푸시 필요 여부 확인

### 5단계: PR 내용 생성

**두 가지 방식 중 하나를 사용합니다:**

#### A. plan.yml 기반 PR 생성 (plan.yml이 있는 경우)

**PR 제목**:
```
<plan.yml의 pr_info.title>
```
- plan.yml에 저장된 제목을 그대로 사용
- SPR 티켓 번호가 있으면 자동으로 추가

**PR 본문 구조 (한글)**:
```markdown
## 요약

<plan.yml의 pr_info.title>

## 배경

<plan.yml의 background.why>

<관련 이슈가 있으면>
관련 이슈: <plan.yml의 background.issue>

## 변경 내용

<plan.yml의 changes.what>

<포함 사항이 있으면>
### 포함된 내용
- <plan.yml의 changes.includes 항목들>

<제외 사항이 있으면>
### 제외된 내용 (향후 작업)
- <plan.yml의 changes.excludes 항목들>

## 테스트

<plan.yml의 testing.scenarios를 체크리스트로>
- [x] <시나리오 1>
- [x] <시나리오 2>

<테스트 노트가 있으면>
### 테스트 노트
<plan.yml의 testing.notes>

## Breaking Changes
<plan.yml의 testing.breaking_changes에 따라>
- breaking_changes: true이면 "있음 - <설명>"
- breaking_changes: false이면 "없음"
```

#### B. git log 기반 PR 생성 (plan.yml이 없는 경우)

**PR 제목 형식**:
```
[SPR-XXXX] 변경사항의 핵심 요약
```

**PR 본문 구조 (한글)**:
```markdown
## 배경
- 이 작업이 필요한 이유 (간단히)
- 해결하려는 문제나 구현하려는 기능 (간단히)

## 작업 내용
각 커밋별 변경사항을 짧게 요약:
- 커밋 1: 무엇을 변경했는지 간단히
- 커밋 2: 무엇을 추가/수정했는지 간단히
- 커밋 3: 무엇을 리팩토링했는지 간단히

## 테스트 방법
리뷰어가 변경사항을 검증할 수 있는 방법:
1. 로컬에서 실행할 명령어
2. 확인해야 할 API 엔드포인트
3. 예상 결과

## 리뷰 노트
(이 섹션은 비워둠)
```

**중요 규칙**:
- **모든 PR 내용은 한글로 작성**
- Claude Code 서명을 절대 추가하지 않음
- "🤖 Generated with [Claude Code]" 또는 "Co-Authored-By: Claude" 등의 서명 포함하지 않음

### 6단계: PR 생성
```bash
gh pr create \
  --title "[SPR-XXXX] 제목" \
  --body "$(cat <<'EOF'
[생성된 PR 내용]
EOF
)" \
  --base <베이스-브랜치> \
  --draft  # 기본값: draft PR로 생성 (--no-draft 옵션이 없는 경우)
```

### 7단계: 결과 확인 및 plan.yml 업데이트

**PR 생성 확인:**
- 생성된 PR URL 제공
- PR 번호와 제목 표시
- 리뷰 요청 상태 확인

```bash
# PR URL을 변수에 저장
PR_URL=$(gh pr view --json url -q .url)
```

**plan.yml 업데이트 (plan.yml이 있었던 경우):**

1. **PR URL 기록**
   ```bash
   # plan.yml이 존재하면 PR URL 추가
   if [ -f ".claude/features/${BRANCH}/plan.yml" ]; then
     # PR URL과 생성 시간 추가
     yq eval '.pr_info.link = "'"$PR_URL"'"' -i ".claude/features/${BRANCH}/plan.yml"
     yq eval '.pr_created_at = "'"$(date -u +"%Y-%m-%dT%H:%M:%SZ")"'"' -i ".claude/features/${BRANCH}/plan.yml"
   fi
   ```

2. **업데이트된 plan.yml 예시:**
   ```yaml
   pr_info:
     title: "Google과 GitHub OAuth2 인증 추가"
     link: "https://github.com/user/repo/pull/42"  # ← 자동 추가됨

   pr_created_at: 2025-01-01T15:30:00Z  # ← 자동 추가됨
   ```

3. **결과 출력:**
   ```
   ✅ plan.yml 업데이트 완료

   PR 링크가 plan.yml에 기록되었습니다.
   파일: .claude/features/<브랜치>/plan.yml
   ```

**브라우저에서 PR 열기:**
```bash
open "$PR_URL"
```

## 출력 형식

**성공 시 (plan.yml 기반):**
```
✅ plan.yml 기반 PR 생성 완료!

PR #1234: Google과 GitHub OAuth2 인증 추가
URL: https://github.com/user/repo/pull/1234

✅ plan.yml 업데이트 완료
   PR 링크가 기록되었습니다: .claude/features/feature/user-auth/plan.yml

브라우저에서 PR 페이지를 열고 있습니다...

다음 단계:
- 리뷰어 할당하기
- CI/CD 파이프라인 확인하기
- 코드 리뷰 피드백 기다리기
```

**성공 시 (git log 기반):**
```
✅ PR이 성공적으로 생성되었습니다!

PR #1234: [SPR-3040] 사용자 인증 시스템 개선
URL: https://github.com/indentcorp/backend/pull/1234

브라우저에서 PR 페이지를 열고 있습니다...

다음 단계:
- 리뷰어 할당하기
- CI/CD 파이프라인 확인하기
- 코드 리뷰 피드백 기다리기
```

**오류 처리**:
```
주의사항 발견:
- 커밋되지 않은 변경사항이 있습니다
- 브랜치 이름이 규칙을 따르지 않습니다

계속 진행하시겠습니까? (권장하지 않음)
```

## 품질 보증

### 검증 단계
1. **브랜치 검증**
   - 올바른 네이밍 규칙 준수 확인
   - main/master가 아닌 브랜치에서 작업 중인지 확인

2. **변경사항 검증**
   - 실제 변경사항이 있는지 확인
   - 민감한 정보(비밀번호, API 키)가 포함되지 않았는지 검사

3. **PR 중복 확인**
   - 동일한 브랜치로 이미 열린 PR이 없는지 확인
   - 있다면 업데이트 제안

4. **템플릿 준수**
   - 모든 필수 섹션이 채워졌는지 확인
   - SPR 티켓 번호가 올바르게 포함되었는지 검증

### 모범 사례
- **작은 PR 유지**: 리뷰하기 쉬운 크기로 변경사항 제한
- **명확한 설명**: 기술적 세부사항과 비즈니스 맥락 모두 포함
- **테스트 포함**: 모든 새 기능에 대한 테스트 코드 확인
- **문서 업데이트**: API 변경 시 문서 동기화

## 고급 기능

### 지능적 분석
- 파일 확장자와 경로를 기반으로 변경 유형 자동 감지
- Django 마이그레이션 파일 자동 인식
- 테스트 파일 변경 시 테스트 명령어 자동 제안

### 최적화
- 모든 git 명령을 병렬로 실행하여 속도 향상
- 캐시된 diff 정보 활용
- 불필요한 네트워크 요청 최소화

### 사용자 경험
- 진행 상황 실시간 표시
- 명확한 오류 메시지와 해결 방법 제시
- 기본적으로 draft PR로 생성하여 안전한 작업 지원 (--no-draft 옵션으로 일반 PR 생성 가능)
