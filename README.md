# Agent skills
A collection of skills for AI agents

## Operations

### Available Skills

> **Note:** When creating a new skill, remember to update this list with its installation command (`npx skills add creatuluw/agent-skills --skill <skill-name>`) and description from SKILL.md frontmatter.

Install skills from this repository:

```bash
# Install all skills from this repository
npx skills add creatuluw/agent-skills

# Or install specific skills
npx skills add creatuluw/agent-skills --skill find-skills
npx skills add creatuluw/agent-skills --skill maestro-task-creator
npx skills add creatuluw/agent-skills --skill skill-creator
```

#### Skills in this repository:

- **find-skills** - Helps users discover and install agent skills when they ask questions like "how do I do X", "find a skill for X", "is there a skill that can...", or express interest in extending capabilities

- **skill-creator** - Guide for creating effective skills. Use this skill when you want to create a new skill (or update an existing skill) that extends Claude's capabilities with specialized knowledge, workflows, or tool integrations

- **maestro-task-creator** - Create Auto Run task documents for Maestro with markdown checklists. Use this when you want to create tasks/playbooks for automated execution, need help structuring work into task documents, or want to "create maestro tasks", "make a playbook", "break down into tasks", or "plan auto run workflow"

### Quick Start
```bash
npx skills find [query]    # Search for skills
npx skills add <package>   # Install a skill
npx skills check           # Check for updates
npx skills update          # Update installed skills
```

## Development Workflow

### Creating New Skills

1. **Research** - Use `find-skills` to discover existing skills before creating new ones
2. **Study Templates** - Review `templates/` directory for patterns and best practices
3. **Create** - Use `skill-creator` to build new skills following [skill-rules.md](skill-rules.md)

### Updating Skills

When editing or updating skills:
- Copy old version to `versioning/` folder with timestamp prefix
- Example: `versioning/2024-01-15-myskill-old/`
- Follow all rules in [skill-rules.md](skill-rules.md)

### Key Resources

- **Skill Creator** - `.opencode/skills/skill-creator` - Guide for building skills
- **Templates** - `templates/` - Study before creating new skills
- **Find Skills** - `.opencode/skills/find-skills` - Discover existing capabilities
- **Skill Rules** - `skill-rules.md` - Must-follow rules for all skills

Learn more at https://skills.sh/docs

### Skills Registry

The repository maintains a `skills.json` file that catalogs all skills in `.agents/skills/` with their frontmatter data and goals. This file is automatically updated when skills are created, updated, or deleted.

**Important:** When creating or modifying skills, always update `skills.json` to keep the registry in sync.
