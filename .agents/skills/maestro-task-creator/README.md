# Maestro Task Creator

## Installation

### Via skills.sh CLI

Install using the skills.sh package manager:

```bash
npx skills add creatuluw/agent-skills --skill maestro-task-creator
```

### Manual Installation

1. Navigate to your skills directory (typically `.agents/skills/` or your configured skills folder)
2. Create a new directory called `maestro-task-creator`
3. Copy all skill files (`SKILL.md`, `assets/`, `references/`, `scripts/`) into this directory
4. Ensure `SKILL.md` is in the root directory

For more information on skills.sh CLI, visit https://skills.sh/docs

## Features

- **Structured Task Documents**: Create well-organized Auto Run task documents for Maestro with clear, actionable checklists
- **Spec-Driven Execution**: Build task documents designed for independent AI agent execution in fresh sessions
- **Logical Decomposition**: Break down complex work into manageable, executable tasks with clear dependencies
- **Context Isolation**: Each task includes sufficient context for execution without ambiguity
- **Verification Integration**: Include verification tasks that confirm successful completion
- **Progress Tracking**: Leverage markdown checkboxes for clear completion state tracking
- **Flexible Structure**: Support for both single documents and multi-document playbooks
- **Iterative Refinement**: Create documents that can be reviewed, updated, and re-run

## When to Use

Use this skill when you need to:

- **Create Maestro Auto Run tasks**: Set up automated execution workflows with task documents
- **Structure work into tasks**: Break down complex projects into actionable, executable steps
- **Plan automated workflows**: Design batch processing or automated execution plans
- **Build playbooks**: Create reusable task documents for repetitive workflows
- **Organize multi-stage work**: Separate work into phases (setup, implementation, verification, cleanup)
- **Enable agent handoffs**: Create independent tasks that different AI agents can execute
- **Document procedures**: Convert manual processes into structured checklists

### Ideal Scenarios

- Setting up new feature development with automated testing
- Creating bug fix workflows with verification steps
- Planning deployment procedures with safety checks
- Designing data migration tasks with validation
- Building documentation generation workflows
- Structuring refactoring initiatives

## Usage

### Basic Workflow

1. **Invoke the Skill**: Trigger when planning work or creating task documents
2. **Discuss Requirements**: The skill will ask questions to understand scope, constraints, and success criteria
3. **Review Task Structure**: Validate the proposed task breakdown and organization
4. **Confirm Document**: Review the final task document before saving
5. **Save to Auto Run**: Store the document in your Maestro Auto Run folder for execution

### Task Document Structure

The skill creates documents following this format:

```markdown
# <Descriptive Title>

## Context
[Brief background on what we're doing and why]

## Tasks
- [ ] Setup: Install dependencies and configure environment
- [ ] Implement: Create/modify files as needed
- [ ] Test: Run tests to verify changes
- [ ] Verify: Confirm feature works as expected
- [ ] Cleanup: Remove temporary files or reset state

## Notes
[Assumptions, constraints, or additional context]
```

### Example Invocation

```
User: I need to create a task document for implementing user authentication

Maestro Task Creator: I'll help you create a structured task document. Let me ask a few questions:
1. What authentication method should we use? (JWT, session-based, OAuth, etc.)
2. Which framework are you using? (React, Angular, etc.)
3. Are there existing auth components we should integrate with?
```

### Best Practices

- **One question at a time**: The skill will ask focused questions to build understanding
- **Iterative refinement**: Review and adjust task structure as needed
- **Clear dependencies**: Ensure tasks are ordered correctly based on dependencies
- **Verifiable outcomes**: Include verification tasks after each major change
- **Sufficient context**: Each task should be independently executable

### Playbook vs. Single Document

Choose based on your needs:

**Single Document**: Best for one-time work or simple linear workflows

**Playbook (Multiple Documents)**: Best for:
- Work that benefits from phase separation
- Scenarios needing document looping
- Parallel execution by different agents
- Reusable workflows with different configurations

### Integration with Maestro

Once created, task documents integrate seamlessly with Maestro Auto Run:

1. Save to your configured Auto Run folder
2. Configure Auto Run settings (loop behavior, reset on completion, etc.)
3. Select your AI agent provider (Claude, Codex, etc.)
4. Run automated execution

For Maestro documentation, visit https://docs.runmaestro.ai/autorun-playbooks