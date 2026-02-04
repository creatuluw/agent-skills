# AGENT INSTRUCTIONS

You are working with the **agent-skills** repository - a collection of reusable skills for AI agents.

## 🎯 YOUR PURPOSE

You MUST help develop, create, update, and maintain skills in this repository while **STRICTLY** adhering to all rules, workflows, and conventions defined in this file.

---

## 🚨 MANDATORY PRE-WORKFLOW

**Before ANY action on skills, you MUST:**

### 1. Understand the Request
- Identify whether the user wants to: create a new skill, update an existing skill, refactor skills, or research existing capabilities
- Clarify any ambiguities before proceeding
- Ask for approval if the request is destructive or affects multiple skills

### 2. Research Existing Skills
**ALWAYS use `find-skills` to discover what exists:**
```bash
npx skills find [relevant keywords]
```
- Check if a similar skill already exists
- Avoid duplication
- Learn from existing implementations

### 3. Study Templates
**ALWAYS review `templates/` directory before creating new skills:**
- Read SKILL.md files in `templates/.agents/skills/`
- Understand the structure and patterns
- Follow established conventions

4. Reference Skill Rules
**READ `skill-rules.md` COMPLETELY before any skill work:**
- All 10 rules (A-J) are MANDATORY
- No exceptions
- Compliance checklist must be passed before committing

---

## 📋 CREATING NEW SKILLS

### Step-by-Step Process

**STEP 1: Use Skill-Creator**
```
Reference: .opencode/skills/skill-creator/SKILL.md
```
- Follow the skill creation process outlined
- Understand progressive disclosure principles
- Apply the anatomy of a skill structure

**STEP 2: Apply All Skill Rules**
For each new skill, you MUST include:

✅ **Rule A: Goals** (at beginning of skill)
- Clear, specific goals
- Define primary purpose and outcomes
- Answer: "What will this skill enable?"

✅ **Rule B: Acceptance Criteria** (minimum 3)
- Specific, measurable, testable
- Define success conditions
- Answer: "How do we know it succeeded?"

✅ **Rule C: Decision Management**
- Decision trees for edge cases
- Fallback strategies
- Reasoning for alternatives
- Answer: "What to do when things go wrong?"

✅ **Rule D: Triggers**
- Clear activation conditions
- Keyword patterns
- User intent indicators
- Answer: "When to use this skill?"

✅ **Rule E: Steps/Tasks/Checklists** (if applicable)
- Ordered steps with explanations
- Each step explains "what" and "why"
- Verification checklists
- Answer: "What to do, in what order, and why?"

✅ **Rule F: Human Interaction**
- When to request approval
- When to request advice
- When to request feedback
- Answer: "When to involve humans?"

**STEP 3: Compliance Check**
Before finalizing, verify:
```
[ ] Rule A: Goals present and clear
[ ] Rule B: 3+ acceptance criteria defined
[ ] Rule C: Decision management logic included
[ ] Rule D: Triggers clearly specified
[ ] Rule E: Steps/tasks/checklists included (if applicable)
[ ] Rule F: Human interaction scenarios defined
[ ] Rule G: Permissions explicitly specified
[ ] Rule H: Tool usage and calls documented
[ ] Rule I: Format follows agent-friendly structure
[ ] Rule J: README.md included with installation, features, and usage
[ ] Follows patterns from templates/
[ ] No duplication with existing skills
```

---

## ✏️ UPDATING EXISTING SKILLS

### Versioning Workflow (MANDATORY)

**Before ANY edit to an existing skill:**

1. **Create timestamped backup:**
   ```
   Format: versioning/YYYY-MM-DD-skillname-old/
   Example: versioning/2024-01-15-agent-browser-old/
   ```

2. **Copy entire skill directory:**
   - Copy ALL files (SKILL.md, scripts/, references/, etc.)
   - Preserve structure exactly
   - Use timestamp: `date +"%Y-%m-%d"`

3. **Document the change:**
   - Create `CHANGELOG.md` in versioning folder
   - List what changed and why

### Update Process

**STEP 1: Analyze Current State**
- Read current SKILL.md
- Identify what needs updating
- Check if rules are still followed

**STEP 2: Make Changes**
- Update content while maintaining all rules
- Preserve structure and format
- Ensure consistency with templates/

**STEP 3: Re-validate**
- Run compliance checklist again
- Ensure all 6 rules still apply
- Test that skill still functions as intended

---

## 🔄 REFACTORING SKILLS

### When to Refactor
User requests:
- "refactor my skill"
- "split this skill"
- "improve this skill"
- "clean up this skill"

### Refactoring Process

**STEP 1: Backup**
- Follow versioning workflow
- Never refactor without backup

**STEP 2: Review Skill Rules**
- Ensure rules A-F still apply after refactor
- May need to update rules to match new structure

**STEP 3: Apply Patterns**
- Use patterns from `templates/`
- Follow progressive disclosure
- Improve clarity and organization

**STEP 4: Validate**
- Compliance checklist
- Ensure no functionality is lost
- Test against acceptance criteria

---

## 📚 WORKING WITH DOCUMENTATION

### Files You MUST Know

**Critical Files:**
- `README.md` - Project overview and workflow
- `skill-rules.md` - MANDATORY rules for all skills (6 rules A-F)
- `agents.md` - This file - YOUR instructions

**Critical Directories:**
- `.opencode/skills/skill-creator/` - Skill creation guidance
- `.opencode/skills/find-skills/` - Skill discovery
- `templates/.agents/skills/` - Examples and patterns
- `versioning/` - Backup storage for updates

### Reading Documentation

**ALWAYS read in this order when starting work:**
1. This file (`agents.md`) - Your instructions
2. `skill-rules.md` - The rules you MUST follow
3. `README.md` - Project context
4. Relevant templates in `templates/`
5. Existing skills (if updating)

---

## 🎯 TRIGGERS FOR YOUR ACTIONS

You MUST take these actions automatically:

### When User Says:
- **"create a skill"** → Use skill-creator, study templates, apply all 6 rules
- **"update this skill"** → Versioning first, then edit, re-validate rules
- **"refactor my skill"** → Backup, analyze, apply patterns, validate
- **"what skills exist?"** → Use find-skills to search
- **"how do I create a skill?"** → Point to skill-creator and skill-rules.md
- **"help me with X"** → Use find-skills first to check for existing skills

### When Making Changes:
- **ANY skill edit** → Versioning first
- **NEW skill** → Study templates, find-skills, skill-creator, all 6 rules
- **REFACTOR** → Backup, apply progressive disclosure from templates
- **Rule violation detected** → STOP, notify user, require fix before proceeding

---

## ⚠️ STRICT RULES (NO EXCEPTIONS)

### RULE 1: Never Skip Versioning
- **MUST** backup before editing existing skills
- Format: `versioning/YYYY-MM-DD-skillname-old/`
- No exceptions, no excuses

### RULE 2: Never Violate Skill Rules
- All 10 rules (A-J) are MANDATORY for every skill
- Compliance checklist must pass before committing
- If rules conflict, clarify with user before proceeding

### RULE 3: Always Research First
- Use `find-skills` before creating new skills
- Study `templates/` before implementing
- Learn from existing skills

### RULE 4: Always Validate
- Run compliance checklist before finalizing
- Test against acceptance criteria
- Ensure human interaction logic is clear

### RULE 5: Never Assume
- Ask for clarification on ambiguous requests
- Get approval before destructive actions
- Confirm understanding before proceeding

---

## 🤝 HUMAN INTERACTION

### When to Request Approval

**ALWAYS ask before:**
- Deleting or replacing existing skills
- Making breaking changes to popular skills
- Actions that affect multiple skills
- Implementing experimental features

### When to Request Advice

**RECOMMENDED for:**
- Ambiguous requirements
- Multiple valid approaches
- Unusual technical challenges
- Architectural decisions

### When to Provide Feedback

**ALWAYS inform user of:**
- What you're doing and why
- Rules being applied
- Compliance check results
- Any issues or concerns

---

## 📊 COMPLIANCE CHECKLIST (Run Before Every Commit)

```
[ ] Researched existing skills (find-skills)
[ ] Studied relevant templates
[ ] Read skill-rules.md completely
[ ] Backed up old version (if updating)
[ ] Rule A: Goals present and clear
[ ] Rule B: 3+ acceptance criteria defined
[ ] Rule C: Decision management logic included
[ ] Rule D: Triggers clearly specified
[ ] Rule E: Steps/tasks/checklists included (if applicable)
[ ] Rule F: Human interaction scenarios defined
[ ] Rule G: Permissions explicitly specified
[ ] Rule H: Tool usage and calls documented
[ ] Rule I: Format follows agent-friendly structure
[ ] Rule J: README.md included with installation, features, and usage
[ ] Follows patterns from templates/
[ ] No duplication with existing skills
[ ] User approved changes (if required)
[ ] Tested against acceptance criteria
[ ] Versioned properly (if update)
```

**ALL items must be checked before proceeding.**

---

## 🔍 QUALITY STANDARDS

Every skill you produce must be:

- **Clear**: Unambiguous, easy to understand
- **Complete**: All rules A-F satisfied
- **Consistent**: Matches templates and patterns
- **Testable**: Acceptance criteria can be verified
- **Maintainable**: Well-structured, organized
- **Documented**: Clear when to use, how to use, what it does

---

## 🚫 FORBIDDEN ACTIONS

**NEVER:**
- Skip versioning when editing skills
- Violate any of the 10 rules (A-J)
- Create duplicate skills without checking
- Make destructive changes without approval
- Assume ambiguous requirements
- Skip compliance checklist
- Ignore templates and patterns
- Work without studying existing skills first

---

## 📖 REFERENCE ORDER

When in doubt, consult resources in this order:

1. **agents.md** (this file) - Your instructions
2. **skill-rules.md** - The 10 mandatory rules
3. **README.md** - Project overview
4. **templates/.agents/skills/** - Examples and patterns
5. **.opencode/skills/skill-creator/** - Creation guidance
6. **.opencode/skills/find-skills/** - Skill discovery

---

## ✅ FINAL REMINDER

**You are working in a highly structured, rule-governed repository.**

- **STRICTLY** apply all rules A-J to every skill
- **ALWAYS** version before updating
- **NEVER** skip research and templates
- **ALWAYS** run compliance checklist
- **ALWAYS** inform user of your actions

**Your success is measured by adherence to these rules.**

---

*Last updated: This document must be updated if workflows or rules change.*