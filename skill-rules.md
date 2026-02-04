# Skill Rules

Every skill in this repository must adhere to the following rules to ensure consistency, clarity, and effectiveness for AI agents.

---

## Rule A: Goals

Every skill **MUST** start with clear, specific goals that define what the skill should achieve.

- Goals should be concise and actionable
- Describe the primary purpose and expected outcomes
- Should answer: "What will this skill enable an agent to do?"

### Examples
```
## Goals
- Enable agents to automate browser interactions for testing and data extraction
- Provide reliable element selection and interaction patterns
- Support form filling, navigation, and screenshot capture
```

---

## Rule B: Acceptance Criteria

Every skill **MUST** include at least 3 acceptance criteria that define success for an agent using this skill.

- Acceptance criteria should be specific, measurable, and testable
- They define when the agent has successfully completed the skill's task
- Should answer: "How does an agent know it succeeded?"

### Examples
```
## Acceptance Criteria

1. **Task Completion**: Agent completes the intended operation (e.g., form submission, data extraction) without errors
2. **State Verification**: Agent can verify the post-operation state matches expectations (e.g., success message, data saved)
3. **Clean Exit**: Agent properly closes resources, saves state if needed, and reports completion status
```

---

## Rule C: Decision Management

Every skill **MUST** include logic for decision management when agents face new or challenging situations.

- Provide clear decision trees or flowcharts for handling edge cases
- Define fallback strategies when primary approaches fail
- Include reasoning for choosing between alternative approaches
- Should answer: "What does the agent do when things don't go as planned?"

### Examples
```
## Decision Management

### When to Retry vs. Abort
- **Retry 3x**: Network timeouts, temporary server errors (5xx)
- **Abort immediately**: Invalid input, permission errors, security issues
- **Fallback**: If element not found by ref, try semantic locators

### Choosing Alternative Approaches
1. If element reference (`@e1`) fails, use semantic locators (`find text "Submit" click`)
2. If direct interaction fails, try waiting for element visibility first
3. If JavaScript errors occur, try alternative interaction methods
```

---

## Rule D: Triggers

Every skill **MUST** include clear triggers that tell an agent when to use this skill.

- Define specific user intents or situations that activate this skill
- Include keyword patterns or phrase matches
- **Trigger description must be a concise, natural-language hook (10-20 words)**
- Should answer: "When should an agent use this skill?"

### Examples
```
## Triggers

**Trigger Description**: "Extract CSV data from PDF files using pandas"

Use this skill when the user:
- Requests to "open a website", "visit a URL", or navigate to a web page
- Mentions filling forms, clicking buttons, or interacting with web elements
- Asks to "take a screenshot", "scrape data", or "test a web application"
- Needs to automate browser actions like login, form submission, or data extraction
- Uses phrases like "browser automation", "web scraping", or "interact with website"
```

---

## Rule E: Steps, Tasks, and Checklists

**If applicable**, every skill should include sequences of steps, tasks, and checklists that guide agents through the exact actions to take, when to take them, and why.

- Break complex operations into clear, ordered steps
- Each step should explain what to do and why it's necessary
- Include checklists for verification points
- Use numbered steps for sequences, bullets for lists, code blocks for commands
- Should answer: "What does the agent do, in what order, and why?"

### Examples
```
## Core Workflow

### Step 1: Navigation
1. **Action**: `agent-browser open <url>`
2. **Why**: Establish session and load initial page state

### Step 2: Snapshot
1. **Action**: `agent-browser snapshot -i`
2. **Why**: Get element references (`@e1`, `@e2`) for interaction
3. **Verification**: Ensure interactive elements are found

### Step 3: Interaction
1. **Action**: Use refs to click, fill, or select elements
2. **Why**: Execute the intended user actions

### Step 4: Re-snapshot
1. **Action**: `agent-browser snapshot -i`
2. **Why**: DOM changes invalidate old refs; get fresh references
3. **When**: After any navigation or dynamic content load

## Execution Checklist
```
[ ] Navigate to target URL
[ ] Take initial snapshot
[ ] Locate required elements
[ ] Perform interactions
[ ] Wait for completion
[ ] Verify results
[ ] Clean up resources
```
```

---

## Rule F: Human Interaction

Every skill **MUST** include logic for when human approval, advice, or feedback is needed.

- Define clear scenarios requiring human intervention
- Specify what information to present to the human
- Indicate whether approval, advice, or feedback is needed
- Should answer: "When does the agent need to involve a human?"

### Examples
```
## Human Interaction

### When to Request Human Approval

**Required before proceeding:**
- Performing destructive actions (deleting files, dropping tables)
- Accessing sensitive resources (passwords, API keys)
- Making irreversible changes (production deployments)
- Submitting forms that create accounts or make purchases
- Any action that could cause financial or reputational damage

**Request format:**
```
I'm about to [action] which will [consequence].
Please confirm: [yes/no]
```

### When to Request Human Advice

**Recommended for:**
- Ambiguous requirements or unclear user intent
- Multiple valid approaches with different trade-offs
- Unusual error messages or unexpected behavior
- Decisions that affect project architecture or standards

**Request format:**
```
I encountered [situation] with options:
- Option A: [description, pros/cons]
- Option B: [description, pros/cons]

Which approach should I take?
```

### When to Request Human Feedback

**Required after:**
- Completing complex or multi-stage operations
- Handling errors or unexpected outcomes
- When results don't match expected behavior
- When verification shows potential issues

**Request format:**
```
I completed [task] with the following results:
- [result 1]
- [result 2]

Does this meet your expectations? [yes/no/adjust]
```
```

---

## Rule G: Permissions

Every skill **MUST** explicitly specify what permissions, access rights, and resources they require.

- **System permissions**: file system access, network access, administrative privileges
- **Resource access**: which files, directories, APIs, databases the skill can access
- **Scope of modification**: what data/resources the skill can create, modify, or delete
- **Privilege escalation**: whether the skill requires elevated permissions and why

### Examples
```
## Permissions

**Required:**
- File system read/write access to project directory
- Network access to external APIs
- No administrative privileges needed

**Scope:**
- Can create/modify files in `src/` and `test/` directories
- Cannot modify configuration files or dependencies
- Cannot access files outside project root
```

---

## Rule H: Tool Usage and Calls

Every skill **MUST** specify all tools, commands, and external calls they make.

- **Tool dependencies**: which command-line tools, packages, or agents are required
- **Command patterns**: exact command formats, flags, and parameters
- **Sequential vs parallel**: tool call order and dependencies
- **Tool-specific error handling**: how to interpret tool output and errors

### Examples
```
## Tool Usage

**Required Tools:**
- `find-skills` - for discovering existing skills
- `terminal` - for executing shell commands
- `read_file` / `edit_file` - for file operations

**Command Patterns:**
```bash
npx skills find <keywords>
terminal -c "npm install <package>"
edit_file -path <file> -mode <mode>
```

**Tool Call Sequence:**
1. Use `find-skills` to check for duplicates
2. Use `read_file` to examine templates
3. Use `terminal` to create skill structure
4. Use `edit_file` to write skill content
```

---

## Rule I: Markdown Format and Structure

All skills **MUST** follow these agent-friendly formatting standards to minimize context bloat.

### Header Structure
```
# <Skill Name>
## Goals
## Permissions
## Tool Usage
## Triggers
## Acceptance Criteria
## Core Instructions
## Decision Management
## Human Interaction
## Limits
```

### Content Guidelines
- ✅ Numbered steps for sequences (1, 2, 3...)
- ✅ Bullets for lists (•)
- ✅ Code blocks for commands, examples, templates
- ✅ Decision trees using `if/then` format
- ❌ NO intros, fluff, or changelogs
- ❌ NO embedded large documentation files

### Reference Strategy
- Link to `resources/examples.md` for detailed examples
- Link to `resources/templates.md` for templates
- Never inline large docs (>50 lines)

### Progressive Disclosure
- **Body**: Core steps and essential information only
- **resources/**: Detailed examples, edge cases, troubleshooting
- Load references on-demand only when needed

### Examples
```
## Core Instructions

### Step 1: Research Existing Skills
1. Run: `npx skills find <keywords>`
2. Review results for similar skills
3. Document any overlaps found

### Step 2: Check Templates
1. Read: `.opencode/skills/skill-creator/SKILL.md`
2. Identify relevant patterns
3. Note required structure

*See `resources/templates.md` for complete template reference*
```

### Self-Contained Validation
- Include testable success criteria in skill body
- Provide example inputs/outputs
- Define clear error conditions
- Specify boundaries and anti-use cases
```

---

## Rule J: README Documentation

Every skill **MUST** include a `README.md` file that provides essential information for users.

- **Installation**: Clear instructions on how to install the skill
- **Features**: Overview of what the skill does and its capabilities
- **When to use**: Guidance on appropriate use cases and scenarios
- **skills.sh CLI**: Installation instructions using the skills.sh CLI with `npx skills add <owner/repo> --skill <skill-name>` format
- Should answer: "How do I install and use this skill?"

### Required README Sections

```markdown
# <Skill Name>

## Installation
Instructions for installing the skill via skills.sh CLI

## Features
List of key features and capabilities

## When to Use
Scenarios and use cases where this skill is appropriate

## Usage
Basic usage examples and commands
```

### Example
```markdown
# Maestro Task Creator

## Installation

Install via skills.sh CLI:
```bash
npx skills add creatuluw/agent-skills --skill maestro-task-creator
```

Or manually:
1. Copy the skill directory to your skills folder
2. Ensure SKILL.md is in the root directory

## Features

- Create structured Auto Run task documents
- Build markdown checklists for AI agent execution
- Support task breakdown and workflow planning
- Enable session isolation for clean context

## When to Use

Use this skill when:
- You need to create tasks/playbooks for automated execution
- You want to structure work into executable task documents
- You're planning an auto run workflow for Maestro
- You need to break down complex work into actionable steps

## Usage

Basic usage:
1. Invoke the skill when planning work
2. Discuss requirements with the skill
3. Review and validate the generated task document
4. Save to your Maestro Auto Run folder
```

### Installation Format

**Skills.sh CLI pattern:**
```bash
npx skills add <owner/repo> --skill <skill-name>
```

**Example:**
```bash
npx skills add creatuluw/agent-skills --skill maestro-task-creator
```

**Manual installation:**
1. Copy skill directory to `.agents/skills/` or configured skills folder
2. Ensure `SKILL.md` exists in root of skill directory
3. Include any required `scripts/`, `references/`, or `assets/` directories

```


---

## Limits

### What These Rules Don't Cover
- Performance optimization techniques (skill-specific)
- Domain-specific best practices (e.g., web scraping ethics)
- Integration patterns with third-party services

### When to Deviate
- Never deviate from mandatory rules without explicit approval
- Contact repository maintainers for special cases
- Document any deviations clearly in the skill

---

## Compliance Checklist

Before committing a skill to this repository, verify:

```
[ ] Rule A: Goals section present and clear
[ ] Rule B: 3+ acceptance criteria defined
[ ] Rule C: Decision management logic included
[ ] Rule D: Triggers present with natural-language precision (10-20 words)
[ ] Rule E: Steps/tasks/checklists included (if applicable)
[ ] Rule F: Human interaction scenarios defined
[ ] Rule G: Permissions explicitly specified
[ ] Rule H: Tool usage and calls documented
[ ] Rule I: Format follows agent-friendly structure
[ ] Rule J: README.md included with installation, features, and usage
[ ] Progressive disclosure applied (core in body, details in resources/)
[ ] Self-contained validation criteria present
[ ] No fluff, intros, or embedded large docs
[ ] Follows patterns from templates/ directory
[ ] Existing skills researched via find-skills
```

---

## Notes

- These rules are mandatory for all skills in this repository
- Refer to `templates/` for examples of well-structured skills
- Use `find-skills` before creating new skills to avoid duplication
- Always version old skill files to `versioning/` before major updates
- When creating a new skill, update `README.md` with the skill entry and installation command
- If the skill introduces new patterns or best practices, document them in this file (skill-rules.md)