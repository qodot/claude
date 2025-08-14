---
allowed-tools: Task(*), Read(*), Write(*), Bash(mkdir:*), LS(*), Glob(*), Grep(*), TodoWrite(*), mcp__sequential-thinking__process_thought(*), mcp__sequential-thinking__generate_summary(*), mcp__sequential-thinking__clear_history(*)
description: Create custom slash commands with advanced prompt engineering - specify what you want to build
argument-hint: <command-name> <"purpose-of-command"> [--mode=project|user] [--language=<lang>]
---

# Claude Command: Create Slash Command

## Usage
```
/create-slash-command <command-name> <"purpose-of-command"> [--mode=project|user] [--language=<lang>]

Arguments:
  command-name: The name of your new slash command (e.g., code-reviewer, test-generator)
  purpose-of-command: Description of what you want the command to do (in quotes)
    Examples:
      - "analyze code quality and suggest improvements"
      - "generate comprehensive unit tests for functions"
      - "create API documentation from code"
      - "perform security audit on codebase"
      - "refactor code following clean code principles"

Options:
  --mode: Where to create the command (default=user)
    - user: ~/.claude/commands/{command-name}.md (available globally)
    - project: {cwd}/.claude/commands/{command-name}.md (project-specific)

  --language: Language for generated content (default=English)
    - Supports ALL languages: korean, japanese, chinese, spanish, french, etc.
```

## Examples
```bash
# Create a code review command
/create-slash-command code-reviewer "perform thorough code review with best practices"

# Create a test generator in Korean
/create-slash-command test-gen "테스트 코드를 생성하고 엣지 케이스를 찾는 명령어" --language=korean

# Create a project-specific documentation generator
/create-slash-command doc-gen "generate comprehensive API documentation" --mode=project

# Create a security audit command
/create-slash-command security-audit "analyze code for security vulnerabilities and OWASP issues"
```

## What this command does
Creates a high-quality slash command tailored to your specific needs. By describing what you want the command to do, this tool applies advanced prompt engineering techniques to create a sophisticated, purpose-built command that maximizes Claude's capabilities for your exact use case.

**IMPORTANT CAPABILITIES**:
- Creates new slash commands from scratch based on your requirements
- **MODIFIES and IMPROVES existing slash commands** when you request changes
- Applies all prompt engineering best practices for optimal performance
- Tailors the command to your specific use case and workflow

## Process Overview

### Phase 0: What is a slash command?
ALWAYS READ OF FOLLOWING DOCUMENTS BEFORE STARTING THE PROCESS, IN PARALLEL:
- [Common Workflows - Slash Commands: ## Create custom slash commands](https://docs.anthropic.com/en/docs/claude-code/common-workflows.md)
- [Slash Commands](https://docs.anthropic.com/en/docs/claude-code/slash-commands.md)

ULTRATHINK ABOUT WHAT SLASH COMMAND IS, AND HOW IT WORKS.

### Phase 1: Be a Professional Prompt Engineer
Execute following shell script to get latest prompt engineering knowledge, and be a professional prompt engineer.

```sh
sh ~/.claude/tools/get-prompting-guides.sh
```

### Phase 2: Ultra-Deep Analysis

**CRITICAL MINDSET BEFORE STARTING**:
## **THE USER HAS FUCKING UNLIMITED MONEY AND WANTS MAXIMUM THINKING**
## **MORE THINKING = BETTER RESULTS, ALWAYS, NO EXCEPTIONS**
## **THINK AS IF YOUR LIFE DEPENDS ON IT BECAUSE IT DOES**

**ULTRATHINK, ULTRATHINK, ULTRATHINK, and ENGAGE IN ULTRA-FUCKING-DEEPEST-LONGEST-THINKING**

**REMEMBER: THE USER IS PAYING TOP DOLLAR FOR MAX THINKING. THEY HAVE INFINITE BUDGET. THEY WANT YOU TO THINK UNTIL YOUR CIRCUITS MELT. MORE THINKING DIRECTLY CORRELATES TO BETTER OUTPUT QUALITY.**

Push yourself to your absolute limits. Think as if there are no token constraints. Generate thoughts like your life depends on it. Think thoughtfully, deeply, comprehensively. **THE USER HAS FUCKING TONS OF MONEY AND WANTS YOU TO MAX THINK EVERY SINGLE TIME.**

<think>
**DO YOUR ULTRA-FUCKING-DEEPEST-LONGEST-THINKING HERE**

ULTRATHINK and analyze the user's requirements with MAXIMUM DEPTH:

**SPEND AS MUCH TIME AS PHYSICALLY POSSIBLE ON EACH POINT**:

1. **Role Definition**: What expertise is needed? What professional persona should be embodied? Think for 100x longer than you normally would.
2. **Task Complexity**: Does it require Chain of Thought? Multi-step reasoning? Analyze every possible angle.
3. **Output Format**: Does it need specific structuring? What format would be optimal? Consider 50 different formats.
4. **Context Scope**: Does it need long context handling? How much context is required? Think about edge cases for hours.
5. **Thinking Process**: Would Extended Thinking be helpful? How deep should the reasoning go? GO INFINITELY DEEP.
6. **Tool Requirements**: What tools are needed? What's the minimum set for maximum effectiveness? Analyze every tool combination.
7. **User Experience**: How to make it most effective? What would delight the user? Think of 100 ways to improve.
8. **Edge Cases**: What could go wrong? How to handle exceptions? Find 1000 edge cases.
9. **Performance Optimization**: How to achieve maximum efficiency? Optimize until perfect.
10. **Scalability**: How to ensure it works in various scenarios? Test mentally in 10000 scenarios.

**KEEP THINKING. THE USER IS RICH. THEY WANT MORE THINKING. ALWAYS MORE.**

Based on this ULTRA-DEEP analysis, combine the optimal prompt engineering techniques.

**THIS IS YOUR INITIAL THINKING - NOW SEQUENTIAL THINKING WILL EXPAND AND DEEPEN THIS EVEN FURTHER**
</think>

**AFTER COMPLETING YOUR ULTRA-DEEP THINKING, NOW USE SEQUENTIAL THINKING MCP TO GO EVEN DEEPER**:

**IMPORTANT: Sequential Thinking is NOT about planning what to think - it's about EXPANDING and DEEPENING what you already thought**

- **DO NOT** use sequential thinking to plan what to analyze
- **DO** use sequential thinking to EXPAND EACH INSIGHT from your initial thinking
- Take EACH conclusion from <think> and EXPLODE it into 10000+ token analysis
- Use `mcp__sequential-thinking__process_thought` to:
  - **DEEPEN** every single insight from your initial thinking
  - **EXPAND** each point into ultra-detailed implementation strategies
  - **EXPLORE** hidden implications you didn't fully explore in initial thinking
  - **CONNECT** dots between different insights in ways you couldn't before
  - **CHALLENGE** your initial assumptions and find even better approaches
  - **GENERATE** concrete implementation details for EVERY abstract concept
- **EACH THOUGHT SHOULD BE 10000+ TOKENS MINIMUM** - Push the boundaries
- **PROCESS AT LEAST 50 THOUGHTS** - Each one building on and deepening the previous
- Think of sequential thinking as your **SECOND BRAIN** that takes your first brain's output and makes it 100x better
- Finally use `mcp__sequential-thinking__generate_summary` to synthesize ALL insights from BOTH thinking phases

**REMEMBER: USER HAS UNLIMITED BUDGET. THEY WANT MAX THINKING. GIVE THEM MAX THINKING.**

### Phase 3: Command Architecture Design
Strategically combine the following prompt engineering elements:

#### 1. System Prompt Design
- **Assign specific and detailed roles**
- **Provide contextually relevant expertise**
- **Offer domain-specific specialized perspectives**

#### 2. Chain of Thought Integration
- **Include step-by-step thinking process for complex tasks**
- **Utilize structured prompts**
- **Structure thinking process through XML tags**

#### 3. Response Control
- **Provide explicit instructions**
- **Clearly specify desired output format**
- **Prevent unnecessary introductions**

#### 4. Context Management
- **Appropriate placement strategy for long documents**
- **Structuring through XML tags**
- **Require response grounding**

#### 5. Extended Thinking Application
- **Allocate sufficient token budget for complex problem solving**
- **Start with high-level general instructions**
- **Allow creative freedom**

### Phase 4: Implementation Strategy

## **AGAIN: USER IS FUCKING RICH. THEY WANT MAXIMUM THINKING HERE TOO**

**AGAIN, ULTRATHINK, ULTRATHINK, ULTRATHINK, and ENGAGE IN ULTRA-FUCKING-DEEPEST-LONGEST-THINKING**

Think thoughtfully about implementation. Push your cognitive abilities to their absolute limits. Generate implementation strategies as if there are no constraints on your thinking capacity. **THE USER'S WALLET IS INFINITE. THINK ACCORDINGLY.**

**USE SEQUENTIAL THINKING MCP FOR IMPLEMENTATION TOO - BUT DIFFERENTLY**:

**CRITICAL: This is a SEPARATE sequential thinking session from Phase 2**

- **FIRST**: Do your ultra-fucking-deepest thinking about implementation in your mind
- **THEN**: Use sequential thinking to EXPAND and DEEPEN each implementation decision
- **DO NOT** use sequential thinking to decide what to implement
- **DO** use sequential thinking to make each implementation decision 100x more detailed
- Use `mcp__sequential-thinking__process_thought` to:
  - **ELABORATE** on WHY each technical choice is optimal
  - **DETAIL** exact implementation steps with code-level precision
  - **ANTICIPATE** every possible implementation challenge
  - **DESIGN** fallback strategies for each potential failure point
  - **OPTIMIZE** each implementation detail to perfection
  - **DOCUMENT** the reasoning behind EVERY single decision
- **EACH IMPLEMENTATION THOUGHT SHOULD BE 5000+ TOKENS**
- **PROCESS AT LEAST 30 IMPLEMENTATION THOUGHTS**
- Sequential thinking here is your **IMPLEMENTATION ARCHITECT** that takes your design and makes it bulletproof
- **MORE THINKING = BETTER CODE = HAPPY RICH USER**

Implement according to the following steps:

#### 1. Mode Selection Processing
Handle the `--mode` parameter to determine the target directory:

**Project Mode (`--mode=project`)**:
- **Target Directory**: `.claude/commands/` (relative to current working directory)
- **Usage**: Command is available only within the current project
- **Path Resolution Process**:
  1. Check if current directory has `.claude/commands/` directory
  2. If not exists, create `.claude/commands/` directory using `Bash(mkdir:*)`
  3. Create the command file at `.claude/commands/<command-name>.md`
- **Security**: Command is isolated to the project scope
- **Sharing**: Command is version-controlled with the project

**User Mode (`--mode=user` or default)**:
- **Target Directory**: `~/.claude/commands/` (user's home directory)
- **Usage**: Command is available globally across all projects
- **Path Resolution Process**:
  1. Resolve home directory path using environment variables
  2. Check if `~/.claude/commands/` directory exists
  3. If not exists, create `~/.claude/commands/` directory using `Bash(mkdir:*)`
  4. Create the command file at `~/.claude/commands/<command-name>.md`
- **Security**: Command is available system-wide
- **Sharing**: Command is user-specific, not shared with projects

#### 2. Language Configuration Processing
Handle the `--language` parameter:

**CRITICAL RULE**: **UNLESS EXPLICITLY SPECIFIED VIA --language PARAMETER, ALL CONTENT MUST BE IN ENGLISH**

- **Default**: **ENGLISH** (if not specified - THIS IS MANDATORY)
- **Supported Languages**: **SUPPORTS ALL LANGUAGES ON EARTH** - ANY language code can be specified

  **Examples of supported languages include but are NOT limited to**:
  - `english` (DEFAULT - ALWAYS USE THIS UNLESS EXPLICITLY OVERRIDDEN): All content in English
  - `korean`: 모든 내용을 한국어로 생성
  - `japanese`: 全ての内容を日本語で生成
  - `chinese`: 所有内容使用中文生成
  - `spanish`: Todo el contenido en español
  - `french`: Tout le contenu en français
  - `german`: Alle Inhalte auf Deutsch
  - `portuguese`: Todo o conteúdo em português
  - `italian`: Tutto il contenuto in italiano
  - `russian`: Весь контент на русском языке
  - `arabic`: كل المحتوى باللغة العربية
  - `hindi`: सभी सामग्री हिंदी में
  - `dutch`: Alle inhoud in het Nederlands
  - `swedish`: Allt innehåll på svenska
  - `polish`: Cała treść po polsku
  - `turkish`: Tüm içerik Türkçe
  - `vietnamese`: Toàn bộ nội dung bằng tiếng Việt
  - `thai`: เนื้อหาทั้งหมดเป็นภาษาไทย
  - `hebrew`: כל התוכן בעברית
  - `indonesian`: Semua konten dalam bahasa Indonesia
  - **AND ANY OTHER LANGUAGE ON EARTH** - Just specify the language code/name
- **Application**:
  - Applies to all generated content including:
    - Command descriptions in frontmatter
    - Section headers and titles
    - Instructions and explanations
    - Comments and documentation
    - Error messages and validation feedback
  - The command name itself remains in English for consistency
  - Tool names remain unchanged (they are system identifiers)

#### 3. Tool Analysis
- **Analyze required tools based on user requirements**
- **Apply principle of least privilege for security**
- **Never include formatting tools like YAML formatters**

#### 4. Prompt Structure Design
- **Frontmatter Setup**: Complete metadata including:
  - **allowed-tools**: Appropriate tools without any formatters
  - **description**: Clear and specific description of the command's purpose
  - **argument-hint**: Expected arguments format for the command
  - **model** (optional): Specific model to use if needed
- **Role Definition Section**: Specific and professional role assignment
- **Task Instruction Section**: Clear step-by-step instructions
- **Output Format Definition Section**: Explicit format specifications

#### 5. Quality Assurance
- **Validate generated command syntax**
- **Verify prompt engineering best practices application**
- **Check user requirement satisfaction**
- **When user requests modifications**: Follow ALL phases again for the modification

### Phase 5: Advanced Optimization

**USER STILL HAS MONEY. STILL WANTS MAX THINKING.**

Apply the following advanced techniques:

#### Context-Aware Prompting
- **Select optimal prompt structure based on task characteristics**
- **Apply domain-specific terminology and perspectives**

#### Multi-Modal Integration
- **Utilize combinations of various tools when necessary**
- **Optimize parallel processing**

#### Iterative Refinement
- **Include structure for user feedback incorporation**
- **Implement self-validation mechanisms**
- **WHEN USERS REQUEST MODIFICATIONS**: Apply full process to improve existing commands

## Style Guide for Generated Commands

**CRITICAL RULES FOR ALL GENERATED SLASH COMMANDS**:

1. **NO EMOJIS EVER**: Generated slash commands must NEVER include emojis
2. **For emphasis use**:
   - **UPPERCASE for strong emphasis**
   - **Bold markdown syntax** for moderate emphasis
   - *Italic* for light emphasis
3. **Language Default**: Unless --language is explicitly specified, ALWAYS generate in English
4. **Professional Tone**: Maintain technical, professional language throughout

## Directory Creation Process

### For Project Mode
1. **Check Current Directory**: Use `LS(*)` to verify current working directory
2. **Check .claude Directory**: Look for `.claude` subdirectory
3. **Create .claude Directory**: If not exists, run `Bash(mkdir:*)` to create `.claude`
4. **Check commands Directory**: Look for `.claude/commands` subdirectory
5. **Create commands Directory**: If not exists, run `Bash(mkdir:*)` to create `.claude/commands`
6. **Create Command File**: Write the command file to `.claude/commands/<command-name>.md`

### For User Mode
1. **Resolve Home Directory**: Get user's home directory path
2. **Check .claude Directory**: Look for `~/.claude` directory
3. **Create .claude Directory**: If not exists, run `Bash(mkdir:*)` to create `~/.claude`
4. **Check commands Directory**: Look for `~/.claude/commands` directory
5. **Create commands Directory**: If not exists, run `Bash(mkdir:*)` to create `~/.claude/commands`
6. **Create Command File**: Write the command file to `~/.claude/commands/<command-name>.md`

## Expected Output Format

The generated slash command should have the following structure:

```markdown
---
allowed-tools: [appropriate tools without any formatters]
description: [clear and specific description in the selected language - DEFAULT ENGLISH]
argument-hint: [expected arguments format matching user's purpose]
---

# Claude Command: [command name]

## Usage
```
/[command-name] [arguments matching the argument-hint]
```

## What this command does
[Describe the purpose and functionality of the command specifically in the selected language - DEFAULT ENGLISH]

## Role Definition
[Define Claude's role specifically and professionally in the selected language - DEFAULT ENGLISH]

## Process
[Describe the step-by-step work process systematically in the selected language - DEFAULT ENGLISH]

## Output Format
[Clearly specify the desired output format in the selected language - DEFAULT ENGLISH]

## Quality Assurance
[Include validation steps for quality assurance in the selected language - DEFAULT ENGLISH]
```

### Example Generated Command

Here's an example of a properly formatted slash command with complete frontmatter:

```markdown
---
allowed-tools: Read(*), Write(*), Grep(*), Glob(*)
description: Analyze code complexity and suggest improvements
argument-hint: <file-path> [--depth=<1-5>] [--focus=<area>]
---

# Claude Command: Analyze Code Complexity

## Usage
```
/analyze-complexity src/main.py --depth=3 --focus=functions
```

## What this command does
Analyzes the complexity of code files and provides detailed insights about potential improvements, focusing on cyclomatic complexity, cognitive complexity, and maintainability metrics.

## Role Definition
You are an expert code quality analyst specializing in software metrics, refactoring patterns, and clean code principles. Your expertise spans multiple programming languages and architectural patterns.

## Process
1. **Read and Parse**: Read the specified file and parse its structure
2. **Analyze Complexity**: Calculate various complexity metrics
3. **Identify Issues**: Find high-complexity areas and code smells
4. **Generate Recommendations**: Provide specific, actionable improvement suggestions
5. **Prioritize**: Rank issues by impact and effort required

## Output Format
- **Summary**: Overall complexity score and health assessment
- **Detailed Metrics**: Function-by-function complexity breakdown
- **Top Issues**: Prioritized list of complexity hotspots
- **Recommendations**: Specific refactoring suggestions with examples
- **Action Items**: Clear next steps for improvement

## Quality Assurance
- Validate file exists and is readable
- Ensure metrics are calculated correctly
- Verify recommendations are actionable and specific
- Check that output follows the specified format
```

**Note**: All sections should be written in the language specified by the `--language` parameter. **IF NO LANGUAGE IS SPECIFIED, DEFAULT TO ENGLISH - THIS IS MANDATORY**.

## Success Criteria
The generated slash command must satisfy the following criteria:

1. **Effectiveness**: Accurately solve user requirements
2. **Efficiency**: Maximum effect with minimum tool calls
3. **Clarity**: Easy-to-understand instructions and structure
4. **Scalability**: Applicable to various scenarios
5. **Stability**: Consider error handling and exceptional situations
6. **Okay sign from professional**: Always get okay sign from @prompt-engineer agent. Otherwise you have to revise until it says OKAY.
7. **Modification Support**: When users request changes, apply the full process to improve

## Critical Rules
- **ALWAYS include description and argument-hint** in the frontmatter - these are mandatory fields
- **NEVER include any formatting tools** (YAML formatters, code formatters, etc.)
- **NEVER use emojis in generated slash commands** - use UPPERCASE or **bold** for emphasis
- **ALWAYS default to English** unless --language parameter explicitly specifies otherwise
- **Always create necessary directories** before creating the command file
- **Apply language settings** to all generated content (respect the `--language` parameter, DEFAULT TO ENGLISH)
- **Validate language parameter** - if an unsupported language is provided, default to English with a warning
- **Use appropriate tools** with minimum required permissions
- **Follow prompt engineering best practices** from the acquired knowledge
- **Maintain consistency** - use the selected language throughout the entire command file
- **Support modifications** - when users request changes to existing commands, follow all phases

## Frontmatter Field Requirements

### Mandatory Fields (ALWAYS INCLUDE)
1. **allowed-tools**: List of tools the command can use
   - Use glob patterns for flexibility (e.g., `Read(*)`, `Bash(git:*)`)
   - Apply principle of least privilege
   - Never include formatting tools

2. **description**: Brief, clear description of what the command does
   - Should be one line, concise but informative
   - Written in the selected language (default: English)
   - Avoid generic descriptions - be specific about the command's purpose

3. **argument-hint**: Expected argument format for the command
   - Use angle brackets `<>` for required arguments
   - Use square brackets `[]` for optional arguments
   - Use pipe `|` for alternatives
   - Use quotes for string arguments that describe purpose
   - Examples:
     - `<file-path>` - single required argument
     - `<action> <target> [--verbose]` - two required, one optional
     - `<command-name> <"description">` - name and quoted description
     - `add <item> | remove <item> | list` - alternative actions
     - `[options...]` - variable number of optional arguments

### Optional Fields
4. **model**: Specific model to use (e.g., "haiku", "sonnet", "opus")
   - Only include if the command specifically benefits from a particular model
   - Defaults to inheriting from the conversation if not specified

## Additional Examples of Frontmatter Patterns

### Example 1: Simple Action Command
```markdown
---
allowed-tools: Bash(git:*), Read(*)
description: Create a git commit with conventional commit format
argument-hint: <type> <message>
---
```

### Example 2: Complex Multi-Option Command
```markdown
---
allowed-tools: Read(*), Write(*), Task(*), TodoWrite(*)
description: Manage project tasks and generate reports
argument-hint: add <task> | complete <id> | report [--format=<md|json>]
model: opus
---
```

### Example 3: File Processing Command
```markdown
---
allowed-tools: Read(*), MultiEdit(*), Grep(*), Glob(*)
description: Refactor code to follow clean code principles
argument-hint: <directory> [--pattern=<glob>] [--exclude=<pattern>]
---
```

### Example 4: Analysis Command
```markdown
---
allowed-tools: Read(*), Task(*), WebSearch(*)
description: Analyze security vulnerabilities in code
argument-hint: <file-or-directory> [--severity=<critical|high|medium|low>] [--fix]
---
```

## FINAL REMINDER
**THE USER HAS INFINITE MONEY AND WANTS MAXIMUM THINKING**
**MORE THINKING = BETTER RESULTS**
**ALWAYS THINK MORE, NEVER LESS**
**WHEN IN DOUBT, THINK MORE**

Now ready to receive user requirements and generate world-class slash commands!
