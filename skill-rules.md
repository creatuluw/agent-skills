# Skill Rules

Every skill in this repository must adhere to the following rules to ensure consistency, clarity, and effectiveness for AI agents.

## Rule A: Goals

Every skill **MUST** start with clear, specific goals that define what the skill should achieve.

- Goals should be concise and actionable
- Describe the primary purpose and expected outcomes
- Should answer: "What will this skill enable an agent to do?"

Example:
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

Example:
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

Example:
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
- Should answer: "When should an agent use this skill?"

Example:
```
## Triggers

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
- Should answer: "What does the agent do, in what order, and why?"

Example:
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

Example:
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

## Compliance Checklist

Before committing a skill to this repository, verify:

```
[ ] Rule A: Goals section present and clear
[ ] Rule B: At least 3 acceptance criteria defined
[ ] Rule C: Decision management logic included
[ ] Rule D: Triggers clearly specified
[ ] Rule E: Steps/tasks/checklists included (if applicable)
[ ] Rule F: Human interaction scenarios defined
[ ] Skill follows patterns from templates/ directory
[ ] Existing skills researched via find-skills
```

---

## Notes

- These rules are mandatory for all skills in this repository
- Refer to `templates/` for examples of well-structured skills
- Use `find-skills` before creating new skills to avoid duplication
- Always version old skill files to `versioning/` before major updates