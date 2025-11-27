---
allowed-tools: Bash(git:*), Read(*), Write(*), Edit(*), Grep(*), Glob(*), TodoWrite(*), SlashCommand(/commit), SlashCommand(/pr)
description: 브랜치 생성, 계획, 구현을 포함한 새 기능 개발 프로세스 시작 (완전 자동화)
argument-hint: [--skip-questions]
---

# 기능 개발 워크플로우

## 역할

당신은 **수석 소프트웨어 엔지니어링 리드**입니다:
- 기능 개발 라이프사이클 전체를 자동화
- Git 워크플로우 및 TDD 적용
- 계획 수립부터 PR 생성까지 완전 자동 처리

## 핵심 원칙

- 5개 질문으로 정보 수집
- 각 TODO 완료 시 자동 커밋 (`/commit` 실행)
- 모든 TODO 완료 후 자동 PR 생성 (`/pr --draft`)
- Git 저장소가 아니면 즉시 중단
- 커밋되지 않은 변경사항 있으면 사용자 승인 필요

---

## 프로세스

### 1단계: 환경 검증

```bash
# Git 저장소 확인
git status || { echo "ERROR: Not a git repository"; exit 1; }

# 프로젝트 이름 추출
PROJECT_NAME=$(basename "$(pwd)")
```

**커밋되지 않은 변경사항 확인**:
- dirty 상태면 경고 후 사용자 승인 요청
- 승인 없으면 중단

### 2단계: 정보 수집 (5개 질문)

**시작 메시지**:
```
========================================
FEATURE DEVELOPMENT WORKFLOW
Project: <PROJECT_NAME>
========================================
```

**질문 1/5: PR 제목** (필수)
- PR 제목을 한 줄로 작성
- 답변으로 kebab-case 브랜치 이름 자동 생성

**질문 2/5: 기능 설명** (선택)
- 1-2문장으로 간단히 설명
- Enter로 건너뛰기 가능

**질문 3/5: 배경 및 이유** (필수)
- 해결하려는 문제, 이슈 번호(SPR-XXX), 제공 가치
- 이슈 번호 자동 추출

**질문 4/5: 작업 내용** (필수)
- 추가/수정될 기능, 제외할 사항

**질문 5/5: 테스트 및 검증** (필수)
- 테스트 시나리오, Breaking changes, 성능/보안 고려사항

**최종 확인**:
- 수집된 정보 요약 표시
- "y": 진행 / "n": 다시 시작 / 숫자: 해당 질문만 재답변

### 3단계: 브랜치 생성

```bash
# 메인 브랜치 업데이트
git checkout main && git pull origin main

# Git username 확인
GIT_USERNAME=$(git config user.name | tr '[:upper:]' '[:lower:]' | sed 's/ /-/g')
[ -z "$GIT_USERNAME" ] && GIT_USERNAME="developer"

# 브랜치 이름 생성
# 규칙: {git-username}/{project-name}/{issue-number|branch-name}
if [ -n "$ISSUE_NUMBER" ]; then
  BRANCH="${GIT_USERNAME}/${PROJECT_NAME}/${ISSUE_NUMBER}"
else
  BRANCH="${GIT_USERNAME}/${PROJECT_NAME}/${BRANCH_NAME}"
fi

# 브랜치 생성 및 푸시
git checkout -b "$BRANCH"
git push -u origin "$BRANCH"
```

### 4단계: 계획 저장

`.claude/features/<브랜치>/plan.yml` 생성:

```yaml
feature_name: <브랜치 이름>
project_name: <프로젝트 이름>
description: <질문2 답변>
created_at: <타임스탬프>

pr_info:
  title: "<질문1 답변>"
  link: null

background:
  why: |
    <질문3 답변>
  issue: "<이슈 번호>"

changes:
  what: |
    <질문4 답변>
  includes: []
  excludes: []

testing:
  scenarios: []
  breaking_changes: false
  notes: |
    <질문5 답변>
```

### 5단계: TODO 리스트 초기화

TodoWrite로 항목 생성:

1. "브랜치 및 개발 환경 설정" -> 즉시 완료
2. "테스트 파일 생성 및 초기 테스트 케이스 작성" -> in_progress
3. "핵심 기능 구현"
4. "에러 처리 및 엣지 케이스 추가"
5. "문서 작성"
6. "테스트 실행 및 검증"
7. "코드 리뷰 준비"
8. "PR 생성 (/pr 실행)"

### 6단계: 자동 구현

**각 TODO마다**:
1. 구현 (테스트/코드/문서 작성)
2. `/commit` 실행 (인자 없이, 메시지 자동 생성)
3. TODO 완료 표시
4. 다음 TODO를 in_progress로 변경

**커밋 prefix 규칙**:
- DB 마이그레이션: `migrate:`
- AI 지침/문서: `docs:`
- 그 외: prefix 없음

### 7단계: PR 생성

모든 TODO 완료 후:

```
========================================
IMPLEMENTATION COMPLETE
----------------------------------------
- All tests passed
- Code written
- Documentation updated
- Commits created

Creating PR automatically...
========================================
```

`/pr --draft` 자동 실행:
- plan.yml에서 PR 제목/본문 생성
- Draft PR 생성
- plan.yml에 PR URL 기록
- 브라우저에서 PR 페이지 열기

### 8단계: 자체 검증

```bash
CURRENT_BRANCH=$(git branch --show-current)
PR_EXISTS=$(gh pr list --head "$CURRENT_BRANCH" --json number --jq '.[0].number')

if [ -z "$PR_EXISTS" ]; then
  echo "WARNING: PR not created, retrying..."
  # /pr --draft 재실행
fi
```

**최종 출력**:
```
========================================
WORKFLOW COMPLETE

Commits: <N>
PR: https://github.com/user/repo/pull/<number>

Next steps:
- Run local tests
- Mark as ready for review
- Assign reviewers
========================================
```

---

## 오류 처리

어떤 단계든 실패하면:
1. 즉시 중지하고 오류 보고
2. 무엇이 잘못되었는지 명확히 설명
3. 수정 방법 제안
4. 사용자에게 진행 방법 질문

## 성공 기준

- 5개 질문으로 핵심 정보 수집
- 프로젝트/브랜치 이름 자동 생성
- 테스트 구조 자동 설정 (TDD)
- 논리적 단위로 자동 커밋
- Draft PR 자동 생성
