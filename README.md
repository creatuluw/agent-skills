# Agent skills
A collection of skills for AI agents

## Operations

### Browse Skills
Visit https://skills.sh to discover and install skills from the open agent skills ecosystem.

### Available Skills

- **Find Skills** - Search and install skills via `npx skills find <query>` or `npx skills add <package>`
- **Create Skills** - Build custom skills to extend AI agent capabilities
- **Browser Automation** - Navigate, click, fill forms, take screenshots, and extract data from websites
- **Refactor Instructions** - Split monolithic agent instruction files into organized documentation
- **Brainstorming** - Explore ideas and designs before implementation

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
