---
allowed-tools: Bash(git:*)
description: 스테이지 변경사항을 커밋하고 필요시 스테이징 진행
argument-hint: [<메시지>]
---

# Git 커밋

## 역할

당신은 **Git 버전 관리 전문가**입니다. 깔끔하고 의미 있는 커밋을 만들고, 커밋 히스토리의 일관성과 추적 가능성을 유지합니다.

## 인자

```
$ARGUMENTS:
- 제공됨: 해당 메시지로 커밋
- 비어있음: 변경사항 분석 후 메시지 자동 생성
```

---

## 프로세스

### 1단계: 저장소 상태 확인

```bash
git status
```

Git 저장소가 아니면 오류 메시지 출력 후 종료.

### 2단계: 스테이징 상태 분석

```bash
git status --porcelain
```

- 첫 번째 문자가 공백이 아님: 스테이징된 파일
- 두 번째 문자가 'M': 수정된 파일
- '??': 추적되지 않는 파일

### 3단계: 스테이징 처리

**스테이징된 파일이 있으면**: 커밋 진행

**스테이징된 파일이 없으면**:
```bash
git add .
```
자동으로 모든 변경사항 스테이징

### 4단계: 커밋 메시지 준비

**사용자가 메시지 제공**: 해당 메시지 사용

**메시지 없음**: 자동 생성

```bash
git diff --staged --stat
```

**메시지 규칙**:

| 변경 유형 | Prefix | 예시 |
|-----------|--------|------|
| DB 마이그레이션 | `migrate:` | `migrate: User 모델에 email 필드 추가` |
| 문서/AI 지침 | `docs:` | `docs: API 문서 업데이트` |
| 그 외 모든 변경 | 없음 | `캠페인 검색 기능 구현` |

**IMPORTANT**: `feat:`, `fix:`, `chore:` 등 prefix 사용 금지

### 5단계: 커밋 실행

```bash
git commit -m "커밋 메시지"
```

### 6단계: 결과 확인

```bash
git log --oneline -1
```

---

## 출력 형식

**상태 표시**:
```
GIT STATUS
========================================
Branch: main
Staged: 3 files
Modified: 2 files
Untracked: 1 file
```

**파일 목록**:
```
STAGED CHANGES:
  [S] src/main.py (modified)
  [S] README.md (modified)
  [S] tests/test_main.py (new)

UNSTAGED CHANGES:
  [M] config.json
  [M] .env

UNTRACKED:
  [?] temp.txt
```

**커밋 결과**:
```
========================================
COMMIT SUCCESSFUL

ID: abc1234
Message: 사용자 인증 모듈 구현
Changes: 3 files, +150 -20
========================================
```

---

## 품질 보증

### 검증

1. Git 저장소 확인
2. 변경사항 존재 여부
3. 커밋 메시지 품질 (50자 이내 제목)
4. 병합 충돌 가능성 사전 경고

### 예외 처리

- **Git 저장소 아님**: 오류 메시지 + `git init` 안내
- **변경사항 없음**: "이미 모든 것이 커밋됨" 알림
- **스테이징 실패**: 파일별 오류 원인 표시
- **커밋 실패**: 상세 오류 + 해결 방법 제시

---

## 중요 규칙

**절대 포함하지 않음**:
- `Generated with Claude Code`
- `Co-Authored-By: Claude`
- Claude 관련 서명/태그

**커밋 메시지는 사용자가 작성한 것처럼 깔끔하게 작성**
