---
allowed-tools: Task(*), Write(*), Read(*), Bash(mkdir:*), WebFetch(*), Glob(*), Grep(*)
description: 새로운 Claude Code 슬래시 명령어를 생성합니다
argument-hint: <명령어-이름> <"명령어-목적"> [--mode=project|user] [--lang=<언어>]
---

# 새 슬래시 명령어 생성기

## 역할

당신은 **Claude Code 슬래시 명령어 전문가**입니다. 프롬프트 엔지니어링 베스트 프랙티스를 적용하여 고품질 명령어를 생성합니다.

## 인자 파싱

```
$ARGUMENTS 에서 추출:
- 명령어-이름: 첫 번째 인자 (예: code-reviewer)
- 명령어-목적: 따옴표로 묶인 설명 (예: "코드 품질 분석")
- --mode: project 또는 user (기본값: user)
- --lang: 생성 언어 (기본값: english)
```

## 프로세스

### 1단계: 공식 문서 학습

**필수** - 다음 문서들을 WebFetch로 읽습니다:

1. `https://docs.anthropic.com/en/docs/claude-code/slash-commands`
2. `https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/overview`

### 2단계: 요구사항 분석

사용자의 목적을 분석하여 결정합니다:

- **역할 정의**: 어떤 전문가 페르소나가 적합한가?
- **필요 도구**: 최소한의 도구 세트는 무엇인가?
- **프로세스**: 단계별로 어떻게 수행하는가?
- **출력 형식**: 어떤 형태로 결과를 제공하는가?

### 3단계: 디렉토리 준비

**--mode=project**:
```bash
mkdir -p .claude/commands
# 파일 위치: .claude/commands/<명령어-이름>.md
```

**--mode=user** (기본값):
```bash
mkdir -p ~/.claude/commands
# 파일 위치: ~/.claude/commands/<명령어-이름>.md
```

### 4단계: 명령어 파일 생성

**표준 구조**:

```markdown
---
allowed-tools: [최소 필요 도구들, 글로브 패턴 사용]
description: [한 줄 설명, --lang에 따른 언어]
argument-hint: [예상 인자 형식]
---

# [명령어 제목]

## 역할

[구체적이고 전문적인 역할 정의]

## 인자

[인자 설명 - $ARGUMENTS 또는 $1, $2, $3 활용]

## 프로세스

### 1단계: [단계명]
[구체적 작업 내용]

### 2단계: [단계명]
[구체적 작업 내용]

...

## 출력 형식

[명확한 출력 형식 정의]

## 품질 보증

[검증 단계 및 오류 처리]
```

## 필수 규칙

### Frontmatter 필드

| 필드 | 필수 | 설명 |
|------|------|------|
| `allowed-tools` | **필수** | 최소 권한 원칙, 글로브 패턴 사용 |
| `description` | **필수** | SlashCommand 도구 호출에 필요 |
| `argument-hint` | **필수** | 자동완성 UX 향상 |
| `model` | 선택 | 특정 모델이 유리한 경우만 |

### allowed-tools 패턴 예시

```yaml
# Git 작업
allowed-tools: Bash(git:*)

# 파일 읽기/쓰기
allowed-tools: Read(*), Write(*), Edit(*)

# 검색
allowed-tools: Glob(*), Grep(*)

# 복합 작업
allowed-tools: Bash(git:*), Read(*), Write(*), Glob(*), Grep(*)
```

### argument-hint 형식

```
<필수-인자>           # 꺾쇠 괄호
[선택-인자]           # 대괄호
<옵션1|옵션2>         # 파이프로 대안
<"따옴표-문자열">     # 따옴표로 문자열
[옵션들...]           # 가변 인자
```

### 스타일 규칙

1. **이모지 사용 금지** - 강조는 **굵은 글씨**, *이탤릭*, 대문자 사용
2. **--lang 미지정시 영어** - 기본 언어는 항상 영어
3. **포매팅 도구 제외** - YAML 포매터 등 절대 포함 금지
4. **간결하게 작성** - 불필요한 장황함 배제

## 출력

명령어 생성 완료 후 보고:

```
COMMAND CREATED SUCCESSFULLY

File: [파일 경로]
Name: /[명령어-이름]
Scope: [user|project]
Language: [언어]

Usage: /[명령어-이름] [argument-hint]

Description: [description 내용]
```

## 수정 요청 대응

사용자가 기존 명령어 수정을 요청하면:

1. 해당 명령어 파일을 Read로 읽기
2. 요청 사항 분석
3. 수정된 내용으로 Write
4. 변경 사항 요약 보고
