---
allowed-tools: Bash(git:*), Bash(gh:*), Bash(open:*), Read(*), Grep(*), Edit(*)
description: 현재 브랜치를 푸시하고 GitHub PR을 작성합니다
argument-hint: [--no-draft] [--base=<브랜치>]
---

# GitHub Pull Request 생성

## 역할

당신은 **Git 워크플로우 및 GitHub 협업 전문가**입니다. Django 백엔드 프로젝트의 구조와 규칙을 이해하고, 효과적인 PR을 작성합니다.

## 인자

```
$ARGUMENTS 파싱:
--no-draft    : 일반 PR로 생성 (기본값: draft)
--base=<branch>: 베이스 브랜치 지정 (기본값: main)
```

---

## 프로세스

### 1단계: 상태 파악

**병렬 실행**:

```bash
# 현재 브랜치
git rev-parse --abbrev-ref HEAD

# 상태 확인
git status

# 변경 내용
git diff --staged --stat
git diff main...HEAD --stat

# 커밋 히스토리
git log main..HEAD --oneline

# 원격 동기화 상태
git status -sb
```

**plan.yml 확인**:
```bash
BRANCH=$(git rev-parse --abbrev-ref HEAD)
PLAN_FILE=".claude/features/${BRANCH}/plan.yml"

if [ -f "$PLAN_FILE" ]; then
  echo "plan.yml found - using feature plan"
else
  echo "No plan.yml - analyzing git log"
fi
```

### 2단계: 브랜치 정보 분석

- 브랜치 이름에서 SPR 티켓 번호 추출 (예: SPR-3040)
- 규칙 미준수 시 경고
- 베이스 브랜치와의 차이점 분석

### 3단계: 변경사항 분류

| 유형 | 설명 |
|------|------|
| 기능 추가 | 새 API, 모델, 서비스 |
| 버그 수정 | 오류 수정, 예외 처리 |
| 리팩토링 | 구조 개선, 성능 최적화 |
| 테스트 | 테스트 코드 추가/수정 |
| 문서화 | 문서 업데이트 |

### 4단계: 브랜치 푸시

```bash
git push -u origin <현재-브랜치>
```

### 5단계: PR 내용 생성

#### A. plan.yml 기반 (plan.yml 있는 경우)

**제목**: `<plan.yml의 pr_info.title>`

**본문**:
```markdown
## 요약

<pr_info.title>

## 배경

<background.why>

관련 이슈: <background.issue>

## 변경 내용

<changes.what>

### 포함된 내용
- <changes.includes 항목들>

### 제외된 내용 (향후 작업)
- <changes.excludes 항목들>

## 테스트

- [x] <testing.scenarios 항목들>

### 테스트 노트
<testing.notes>

## Breaking Changes

<testing.breaking_changes: true면 "있음" / false면 "없음">
```

#### B. git log 기반 (plan.yml 없는 경우)

**제목**: `[SPR-XXXX] 변경사항 핵심 요약`

**본문**:
```markdown
## 배경

- 이 작업이 필요한 이유
- 해결하려는 문제 또는 구현 기능

## 작업 내용

각 커밋별 변경사항 요약:
- 커밋 1: 변경 내용
- 커밋 2: 변경 내용

## 테스트 방법

1. 실행할 명령어
2. 확인할 엔드포인트
3. 예상 결과

## 리뷰 노트

(비워둠)
```

### 6단계: PR 생성

```bash
gh pr create \
  --title "[SPR-XXXX] 제목" \
  --body "$(cat <<'EOF'
[생성된 PR 내용]
EOF
)" \
  --base <베이스-브랜치> \
  --draft  # --no-draft 옵션 없으면 draft로 생성
```

### 7단계: plan.yml 업데이트 및 브라우저 열기

```bash
PR_URL=$(gh pr view --json url -q .url)

# plan.yml이 있으면 PR URL 기록
if [ -f "$PLAN_FILE" ]; then
  # PR URL 추가
fi

# 브라우저에서 열기
open "$PR_URL"
```

---

## 출력 형식

**성공 (plan.yml 기반)**:
```
========================================
PR CREATED (from plan.yml)

PR #1234: <제목>
URL: https://github.com/user/repo/pull/1234

plan.yml updated with PR link

Opening in browser...

Next steps:
- Assign reviewers
- Check CI/CD pipeline
- Wait for code review
========================================
```

**성공 (git log 기반)**:
```
========================================
PR CREATED

PR #1234: [SPR-3040] <제목>
URL: https://github.com/indentcorp/backend/pull/1234

Opening in browser...

Next steps:
- Assign reviewers
- Check CI/CD pipeline
- Wait for code review
========================================
```

---

## 품질 보증

### 검증

1. **브랜치 검증**: 네이밍 규칙 준수, main/master가 아닌지 확인
2. **변경사항 검증**: 실제 변경사항 존재, 민감정보 미포함
3. **PR 중복 확인**: 동일 브랜치로 열린 PR 존재 여부
4. **템플릿 준수**: 필수 섹션 충족, SPR 번호 포함

### 모범 사례

- 작은 PR 유지
- 명확한 설명 (기술 + 비즈니스 맥락)
- 테스트 포함
- API 변경 시 문서 동기화

---

## 중요 규칙

**절대 포함하지 않음**:
- Claude Code 서명
- "Generated with Claude Code"
- "Co-Authored-By: Claude"

**모든 PR 내용은 한글로 작성**
