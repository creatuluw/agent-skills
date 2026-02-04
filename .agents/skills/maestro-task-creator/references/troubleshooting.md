# Troubleshooting Maestro Task Documents

This file provides guidance for troubleshooting common issues with Auto Run task documents and playbooks.

---

## Common Issues and Solutions

### Issue: Tasks Are Not Completing

**Symptoms:**
- Auto Run hangs or gets stuck on a task
- Task remains unchecked after execution
- Agent repeatedly fails to complete a task

**Possible Causes:**
1. **Task is too vague or ambiguous**
   - Agent doesn't know exactly what to do
   - Multiple interpretations possible
   - Missing specific file paths or locations

2. **Task requires context not provided**
   - Agent lacks project knowledge
   - Dependencies not explained
   - Assumptions not documented

3. **Task is too large or complex**
   - Single task covers too much work
   - Multiple steps rolled into one
   - Takes longer than 30 minutes to complete

**Solutions:**
```markdown
# Before (too vague):
- [ ] Fix the authentication bug

# After (specific):
- [ ] Fix authentication bug in src/components/Login.tsx where OAuth callback fails with invalid redirect URI
```

```markdown
# Before (too large):
- [ ] Implement full user authentication system with OAuth, session management, and database integration

# After (broken down):
- [ ] Install OAuth dependencies: npm install passport passport-google-oauth20 express-session
- [ ] Create OAuth strategy: Implement src/auth/google.strategy.ts with Google OAuth configuration
- [ ] Setup session middleware: Configure express-session in src/index.ts
- [ ] Add auth routes: Implement /auth/google and /auth/google/callback endpoints
- [ ] Create user model: Define src/models/User.ts with profile fields
```

**Diagnostic Steps:**
1. Check the AI session for error messages or confusion
2. Review the task description for ambiguity
3. Verify context is sufficient in the document
4. Break down large tasks into smaller ones
5. Add verification steps to confirm completion

---

### Issue: Tasks Complete But Work is Incorrect

**Symptoms:**
- Task is marked complete but implementation is wrong
- Agent makes incorrect assumptions
- Work doesn't match requirements or expectations

**Possible Causes:**
1. **Success criteria not clearly defined**
   - No way to verify correctness
   - Multiple valid interpretations
   - Requirements not explicitly stated

2. **Missing or insufficient verification tasks**
   - No tests to validate work
   - No manual verification steps
   - No output checking

3. **Context is misleading or outdated**
   - Outdated assumptions about codebase
   - Incorrect file paths or locations
   - Conflicting information in document

**Solutions:**
```markdown
# Add clear success criteria:
## Success Criteria
- Users can sign in with Google OAuth
- User profile is saved to database correctly
- Session persists across page refreshes
- Logout clears session and redirects to home

# Add verification tasks:
- [ ] Verify Google OAuth flow works end-to-end
- [ ] Check database for saved user record
- [ ] Test session persistence by refreshing page
- [ ] Confirm logout clears session cookie
```

**Diagnostic Steps:**
1. Review the task's verification steps
2. Check if success criteria are measurable
3. Verify context matches current codebase state
4. Add specific tests or checks to validate work
5. Review AI session to understand what was done

---

### Issue: Tasks Have Wrong Dependencies or Order

**Symptoms:**
- Later tasks fail because earlier tasks didn't complete properly
- Tasks execute out of logical order
- Some tasks need others to complete first but are listed earlier

**Possible Causes:**
1. **Dependencies not explicitly stated**
   - Task A requires Task B to complete first
   - No indication of task order importance
   - Parallel execution causes conflicts

2. **Task order doesn't reflect workflow**
   - Testing before implementation
   - Cleanup before setup
   - Integration work before foundation

**Solutions:**
```markdown
# Add dependency notes:
- [ ] Install dependencies: npm install express typescript
- [ ] Initialize project: Run tsc --init to create tsconfig.json
- [ ] Create base structure: Set up folders (src/, tests/, docs/)
- [ ] (Depends on previous tasks) Implement core logic: Write src/index.ts
- [ ] (After implementation) Write tests: Create tests/index.test.ts
- [ ] (After tests pass) Build project: Run npm run build
```

**Task Ordering Best Practices:**
1. **Setup/Installation** → First
2. **Implementation** → Middle
3. **Testing/Verification** → After implementation
4. **Documentation** → After testing passes
5. **Cleanup** → Last
6. **Deployment** → After all verification complete

**Diagnostic Steps:**
1. Review task order for logical flow
2. Identify implicit dependencies
3. Document dependencies in task descriptions
4. Use "Depends on" or "After" prefixes where needed
5. Consider splitting into separate documents for different phases

---

### Issue: Document Context is Insufficient

**Symptoms:**
- Agent asks clarifying questions repeatedly
- Agent makes incorrect assumptions about project
- Implementation doesn't match project conventions

**Possible Causes:**
1. **Missing project background**
   - No overview of what the project is
   - No tech stack information
   - No architectural context

2. **No file or system references**
   - Agent doesn't know where to look
   - No paths to relevant files
   - No indication of system components

3. **Outdated or incorrect assumptions**
   - Context doesn't match current codebase
   - Assumptions about file structure are wrong
   - Project has changed since document was created

**Solutions:**
```markdown
## Context
This document adds OAuth authentication to a React + Node.js application.

**Tech Stack:**
- Frontend: React 18 with TypeScript
- Backend: Node.js with Express
- Database: PostgreSQL
- Authentication: Google OAuth 2.0

**Project Structure:**
- src/components/ - React components
- src/services/ - API and service layer
- src/routes/ - Express route handlers
- src/models/ - Database models
- tests/ - Unit and integration tests

**Key Files:**
- src/index.ts - Express server entry point
- src/App.tsx - React app root
- package.json - Dependencies and scripts

**Assumptions:**
- Google OAuth app already created in Google Cloud Console
- Database connection configured in .env
- Application runs on http://localhost:3000 in dev
```

**Diagnostic Steps:**
1. Review the Context section of the document
2. Check if tech stack is documented
3. Verify file structure and paths are correct
4. Ensure assumptions are explicit and accurate
5. Add examples or references to similar work

---

### Issue: Verification Tasks Are Failing

**Symptoms:**
- Tests fail but implementation seems correct
- Manual verification doesn't match expectations
- Verification tasks are ambiguous or impossible

**Possible Causes:**
1. **Verification tasks are not specific enough**
   - "Test the feature" - how?
   - "Verify it works" - what does "works" mean?
   - "Check for errors" - what errors?

2. **Verification depends on work not yet done**
   - Tests written before implementation
   - Checking files that don't exist yet
   - Verifying features not yet implemented

3. **Verification is manual but requires automation**
   - Complex flows are hard to test manually
   - Multiple scenarios need testing
   - Regression risk is high

**Solutions:**
```markdown
# Before (too vague):
- [ ] Test the authentication

# After (specific):
- [ ] Test authentication by signing in with a test Google account
- [ ] Verify user profile appears in UI after successful login
- [ ] Check database contains user record with correct email
- [ ] Confirm session cookie is set with secure flags
- [ ] Test logout clears session and redirects to login
```

```markdown
# Add automated verification:
- [ ] Run unit tests: Execute npm test -- --testPathPattern=auth
- [ ] Run integration tests: Execute npm run test:integration
- [ ] Run linting: Execute npm run lint
- [ ] Build project: Execute npm run build and verify no errors
```

**Diagnostic Steps:**
1. Review verification tasks for clarity
2. Ensure verification is testable and measurable
3. Verify verification can actually be performed
4. Add both automated and manual verification where appropriate
5. Check if verification depends on correct task ordering

---

### Issue: Tasks Are Too Small or Trivial

**Symptoms:**
- Document has many tiny tasks (e.g., 50+ tasks)
- Tasks take less than 2 minutes each
- Document is hard to navigate and understand
- Agent wastes time on context switching

**Possible Causes:**
1. **Over-decomposition**
   - Breaking simple operations into many tiny steps
   - Creating a task for every file change
   - Listing every npm command as a separate task

2. **Loss of task cohesion**
   - Related actions split across multiple tasks
   - Natural work units broken apart
   - No logical grouping of related work

**Solutions:**
```markdown
# Before (too many small tasks):
- [ ] Create src/components/Auth.tsx
- [ ] Add import for React
- [ ] Add component structure
- [ ] Add state for user
- [ ] Add login function
- [ ] Add logout function
- [ ] Add JSX return
- [ ] Export component

# After (cohesive task):
- [ ] Create Auth component: Implement src/components/Auth.tsx with React functional component containing user state, login/logout functions, and JSX for rendering authentication UI
```

**Task Size Guidelines:**
- **Too small**: < 2 minutes per task
- **Ideal**: 5-15 minutes per task
- **Too large**: > 30 minutes per task

**When to combine:**
- Tasks are tightly coupled (must be done together)
- Tasks are part of a single, cohesive action
- Tasks would create excessive context switching
- Tasks are trivial and better grouped

**Diagnostic Steps:**
1. Count tasks - if > 20 for simple work, may be over-decomposed
2. Review task descriptions for logical grouping
3. Check if tasks naturally belong together
4. Combine related tasks into cohesive units
5. Maintain clear boundaries between different types of work

---

## Maestro-Specific Issues

### Issue: Auto Run Cannot Find Documents

**Symptoms:**
- Documents don't appear in Auto Run dropdown
- Maestro shows "No documents found" message
- Documents are in wrong folder

**Solutions:**
1. Verify documents are in the Auto Run folder configured in Maestro
2. Ensure files have `.md` extension
3. Check file permissions (Maestro needs read access)
4. Refresh the Auto Run panel by clicking the refresh button
5. Verify folder path is correct in Maestro settings

### Issue: Tasks Run but Don't Mark as Complete

**Symptoms:**
- Tasks execute successfully but remain unchecked
- Progress indicator doesn't update
- Document shows no completed tasks

**Solutions:**
1. Check that task format is correct: `- [ ] Task description`
2. Ensure document is saved before running
3. Verify Auto Run has write permissions to modify the document
4. Check if "Reset on Completion" is enabled (creates copy in `Runs/` folder)
5. Review Maestro logs for errors

### Issue: Session Isolation Issues

**Symptoms:**
- Later tasks fail because they don't have context from earlier tasks
- Agent repeats work done in previous tasks
- Tasks expect state from previous sessions

**Understanding Session Isolation:**
- Each task runs in a **fresh AI session** with no memory
- This is intentional and critical for reliable execution
- Tasks must be **independent** and **self-contained**
- Do not rely on tasks having knowledge of previous work

**Solutions:**
```markdown
# Don't do this (assumes session memory):
- [ ] Setup database connection
- [ ] (Agent remembers setup) Create user table

# Do this (each task is independent):
- [ ] Setup database connection: Initialize connection in src/db/connection.ts
- [ ] Create user table: Run SQL script to create users table in src/db/schema/users.sql
```

**When Session Isolation is a Problem:**
- If you need tasks to share state, use a different approach:
  1. Put related tasks in a single, larger task
  2. Use a single AI conversation instead of Auto Run
  3. Store state in files/database that tasks can read

### Issue: Reset on Completion Not Working

**Symptoms:**
- Original document is being modified
- No copies created in `Runs/` folder
- Document state is lost between runs

**Solutions:**
1. Enable "Reset on Completion" in Auto Run configuration
2. Verify `Runs/` folder exists and is writable
3. Check that Maestro has permissions to create files
4. Review Maestro documentation for Reset on Completion behavior
5. Understand that original document should never be modified

---

## Playbook-Specific Issues

### Issue: Playbook Documents Run in Wrong Order

**Symptoms:**
- Documents execute out of intended sequence
- Setup runs after implementation
- Verification runs before implementation

**Solutions:**
1. Reorder documents in the Playbook configuration
2. Use drag-and-drop to set correct order in Auto Run panel
3. Save the Playbook after reordering
4. Use numbered prefixes in filenames (e.g., `01-setup.md`, `02-implement.md`)
5. Verify order before running the Playbook

### Issue: Loop Mode Not Working as Expected

**Symptoms:**
- Playbook stops after first iteration
- Documents don't reset between loops
- Context bleeds between loop iterations

**Solutions:**
1. Enable "Loop Mode" in Playbook configuration
2. Enable "Reset on Completion" for documents that should loop
3. Verify only loopable documents have Reset on Completion enabled
4. Understand that each loop iteration creates a fresh working copy
5. Check that documents are designed to work in loops (independent tasks)

### Issue: Multiple Documents Conflicting

**Symptoms:**
- Documents modify the same files
- Later tasks fail because earlier documents changed things
- Race conditions when documents run in parallel

**Solutions:**
1. **Separate by concern**: Different documents should touch different areas
   - Document 1: Backend tasks
   - Document 2: Frontend tasks
   - Document 3: Documentation tasks

2. **Separate by phase**: Different documents for different phases
   - Document 1: Setup (runs once)
   - Document 2: Implementation (can loop)
   - Document 3: Verification (runs once at end)

3. **Use Git worktrees**: For true parallel execution, create isolated worktrees for each document

4. **Add conflict detection**: Include tasks that check for conflicts before proceeding

---

## Performance and Efficiency Issues

### Issue: Auto Run Takes Too Long

**Symptoms:**
- Tasks complete slowly
- Total execution time is excessive
- Agent seems to struggle with tasks

**Possible Causes:**
1. **Tasks are too large** - Agent gets overwhelmed
2. **Tasks lack context** - Agent spends time searching
3. **Tasks have unclear directions** - Agent tries multiple approaches
4. **Verification is excessive** - Too many checks

**Solutions:**
1. Break down large tasks into smaller, focused ones
2. Add more context to reduce agent exploration time
3. Make task descriptions more specific and actionable
4. Combine redundant verification tasks
5. Use parallel execution when appropriate (with worktrees)

### Issue: Context Window Exhaustion

**Symptoms:**
- Agent runs out of context mid-task
- Tasks are cut off or incomplete
- Agent loses track of what it's doing

**Solutions:**
1. Reduce the amount of context in each task
2. Use references/ folder for large documentation (load only when needed)
3. Break large tasks into smaller ones
4. Move verbose explanations to document Context section
5. Use progressive disclosure: core in tasks, details in Context

---

## Debugging Steps

When an issue occurs, follow this systematic approach:

### 1. Identify the Problem
- What specifically is not working?
- When does the issue occur?
- Is it reproducible?

### 2. Check the Document
- Review task descriptions for clarity
- Verify context is sufficient and accurate
- Check task order and dependencies
- Ensure verification tasks are testable

### 3. Review the AI Session
- Look at the actual AI conversation
- Identify where things went wrong
- Check for error messages or confusion
- Understand what the agent attempted

### 4. Analyze Root Cause
- Is the task description the problem?
- Is the context missing or incorrect?
- Is the task too large or too small?
- Are dependencies not stated?

### 5. Apply Fix
- Rewrite task description for clarity
- Add or update context
- Break down or combine tasks
- Add verification steps
- Document dependencies explicitly

### 6. Test the Fix
- Run the updated document
- Verify the fix resolves the issue
- Check for new issues introduced
- Document what was changed and why

---

## Prevention and Best Practices

### Before Creating Tasks
1. **Understand the work** fully before writing tasks
2. **Review existing patterns** in the codebase
3. **Clarify requirements** with stakeholders if needed
4. **Plan the task structure** before writing

### While Writing Tasks
1. **Be specific** - include file paths, commands, and expected outcomes
2. **Make tasks independent** - each should work in isolation
3. **Add verification** - every implementation needs verification
4. **Order tasks logically** - respect dependencies and workflows

### After Creating Tasks
1. **Review for clarity** - read tasks as if you're the AI agent
2. **Check dependencies** - ensure order makes sense
3. **Test mentally** - walk through executing the tasks
4. **Get feedback** - have someone else review the document

### When Running Tasks
1. **Monitor progress** - watch for stuck or failing tasks
2. **Review sessions** - check how the agent is interpreting tasks
3. **Iterate** - refine tasks based on execution results
4. **Document learnings** - note what worked and what didn't

---

## Getting Help

If you're unable to resolve an issue:

1. **Check Maestro documentation**: https://docs.runmaestro.ai/
2. **Review this troubleshooting guide** for similar issues
3. **Examine example documents** in the `examples/` folder
4. **Consult the community**: Check Maestro Discord or forums
5. **Start simple**: If stuck, break down to minimal working example

---

## Quick Reference

| Issue | Likely Cause | Quick Fix |
|-------|--------------|-----------|
| Tasks not completing | Too vague or large | Break down, add specifics |
| Work is incorrect | No verification | Add test/check tasks |
| Wrong order | Dependencies not stated | Document dependencies explicitly |
| Insufficient context | Missing project info | Add Context section |
| Verification fails | Not specific enough | Add concrete test steps |
| Too many small tasks | Over-decomposed | Combine related tasks |
| Session isolation issues | Tasks not independent | Make tasks self-contained |
| Playbook wrong order | Documents misordered | Reorder in configuration |
| Slow execution | Tasks too large | Break down smaller |
| Context exhaustion | Too much in tasks | Move details to Context |

---

Remember: Well-written task documents are clear, specific, testable, and designed for independent execution in fresh AI sessions. The goal is to provide enough context for the agent to succeed without overwhelming it with unnecessary detail.