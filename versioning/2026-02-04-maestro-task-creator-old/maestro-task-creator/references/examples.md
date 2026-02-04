# Maestro Task Document Examples

This file provides detailed examples of well-structured Auto Run task documents for various scenarios.

---

## Example 1: Feature Implementation

Use this pattern for implementing new features or functionality.

```markdown
# Add User Authentication with OAuth

## Context
Implement OAuth authentication for the application using Google OAuth 2.0. This will allow users to sign in with their Google accounts instead of creating local credentials.

**Tech Stack:**
- Backend: Node.js with Express
- OAuth Library: `passport-google-oauth20`
- Frontend: React with TypeScript
- State Management: Zustand

**Success Criteria:**
- Users can sign in with Google
- User profile data is stored in database
- Sessions are managed securely
- Logout functionality works correctly

## Tasks
- [ ] Install dependencies: Run `npm install passport passport-google-oauth20 express-session dotenv`
- [ ] Configure OAuth credentials: Create `.env` file with `GOOGLE_CLIENT_ID`, `GOOGLE_CLIENT_SECRET`, and `SESSION_SECRET`
- [ ] Create OAuth strategy: Implement `src/auth/google.strategy.ts` with passport configuration
- [ ] Setup session middleware: Configure express-session in `src/index.ts` with secure settings
- [ ] Add auth routes: Implement `/auth/google` and `/auth/google/callback` endpoints in `src/routes/auth.ts`
- [ ] Create user model: Define `src/models/User.ts` with profile fields (id, name, email, avatar)
- [ ] Add database integration: Implement `src/db/user.repository.ts` for user CRUD operations
- [ ] Create auth store: Implement `src/stores/auth.store.ts` for frontend state management
- [ ] Build login component: Create `src/components/Login.tsx` with "Sign in with Google" button
- [ ] Add protected route: Implement `src/components/ProtectedRoute.tsx` to check authentication
- [ ] Update main app: Modify `src/App.tsx` to use auth store and protected routes
- [ ] Add environment validation: Create `src/config/env.ts` to validate required environment variables
- [ ] Write unit tests: Create `src/auth/__tests__/google.strategy.test.ts` for strategy tests
- [ ] Write integration tests: Create `src/routes/__tests__/auth.test.ts` for endpoint tests
- [ ] Test login flow: Manually test sign-in, redirect, and session persistence
- [ ] Test logout: Verify logout clears session and redirects correctly
- [ ] Update documentation: Add OAuth setup instructions to `README.md`
- [ ] Clean up: Remove temporary test files and console.log statements

## Notes
**Assumptions:**
- Google OAuth app is already created in Google Cloud Console
- Database connection is already configured
- Application runs on `http://localhost:3000` in development

**File Locations:**
- All auth code goes in `src/auth/`
- Routes in `src/routes/auth.ts`
- Database operations in `src/db/`
- Frontend components in `src/components/`

**Verification:**
- After implementation, test with a real Google account
- Verify user data is correctly saved in database
- Check that session persists across page refreshes
```

---

## Example 2: Bug Fix

Use this pattern for fixing specific bugs or issues.

```markdown
# Fix: Login Form Not Validating Email Format

## Context
The login form at `src/components/Login.tsx` is not validating email format before submission. Users can submit invalid email addresses, causing errors on the backend and poor user experience.

**Root Cause:**
Email validation is only performed on the server, not on the client.

**Success Criteria:**
- Email field validates format on input
- Shows error message for invalid emails
- Disables submit button when form is invalid
- Server validation remains as fallback

## Tasks
- [ ] Read current implementation: Examine `src/components/Login.tsx` to understand current form structure
- [ ] Choose validation library: Evaluate `zod` vs `react-hook-form` for form validation (prefer zod if no existing form library)
- [ ] Install validation library: Run `npm install zod react-hook-form` if not already installed
- [ ] Create email schema: Define `src/schemas/email.schema.ts` with zod email validation
- [ ] Update login form: Integrate validation into `src/components/Login.tsx`
- [ ] Add error display: Show validation error message below email field
- [ ] Disable submit button: Set `disabled` prop based on form validity
- [ ] Add unit tests: Create `src/components/__tests__/Login.test.tsx` for validation logic
- [ ] Test valid emails: Verify correct email formats (user@example.com, name@domain.co.uk)
- [ ] Test invalid emails: Verify invalid formats are rejected (user, @example.com, user@)
- [ ] Test error messages: Verify clear error messages appear for invalid input
- [ ] Test submit button: Verify button is disabled for invalid forms
- [ ] Verify server validation: Confirm backend still validates as fallback
- [ ] Check for other forms: Search for other forms that need similar validation
- [ ] Update related files: Apply pattern to `src/components/Signup.tsx` if similar issue exists
- [ ] Run test suite: Execute `npm test` to ensure no regressions
- [ ] Manual testing: Test login form in browser with various email formats

## Notes
**Priority: High** - This affects user experience and data integrity

**Impact:**
- May affect other forms in the application
- Should be applied consistently across all email input fields

**Testing Checklist:**
- [ ] Valid email with subdomain (user@mail.example.com)
- [ ] Valid email with numbers (user123@example.com)
- [ ] Invalid: missing @ (userexample.com)
- [ ] Invalid: missing domain (user@)
- [ ] Invalid: spaces in email (user @example.com)
- [ ] Invalid: special characters (user#example.com)
```

---

## Example 3: Refactoring

Use this pattern for code refactoring and cleanup tasks.

```markdown
# Refactor: Replace Callbacks with Async/Await

## Context
The codebase uses outdated callback patterns in `src/services/api.ts`. This makes code difficult to read, debug, and maintain. We need to modernize to async/await pattern.

**Files to Update:**
- `src/services/api.ts` (main API service)
- `src/components/UserProfile.tsx` (consumes API)
- `src/components/PostList.tsx` (consumes API)
- `src/services/__tests__/api.test.ts` (tests)

**Success Criteria:**
- All API calls use async/await
- Error handling uses try/catch
- Tests pass with new pattern
- No breaking changes to function signatures
- Code is more readable and maintainable

## Tasks
- [ ] Analyze current implementation: Read `src/services/api.ts` to understand callback usage
- [ ] Identify callback patterns: Find all functions using callback parameters
- [ ] Create backup branch: Run `git checkout -b refactor-async-await`
- [ ] Refactor getUser function: Convert callback to async/await in `src/services/api.ts`
- [ ] Refactor getPosts function: Convert callback to async/await in `src/services/api.ts`
- [ ] Refactor createPost function: Convert callback to async/await in `src/services/api.ts`
- [ ] Update UserProfile component: Update `src/components/UserProfile.tsx` to await getUser
- [ ] Update PostList component: Update `src/components/PostList.tsx` to await getPosts
- [ ] Add error handling: Wrap API calls in try/catch blocks
- [ ] Update tests: Rewrite `src/services/__tests__/api.test.ts` to use async/await
- [ ] Test getUser: Verify user data is returned correctly
- [ ] Test error handling: Verify errors are caught and handled appropriately
- [ ] Test getUser: Verify user data is returned correctly
- [ ] Test getPosts: Verify posts array is returned correctly
- [ ] Test createPost: Verify post is created and returned
- [ ] Test network errors: Verify error handling for failed requests
- [ ] Run full test suite: Execute `npm test` to ensure no regressions
- [ ] Check for other consumers: Search for other files using these API functions
- [ ] Update any remaining consumers: If found, update to async/await pattern
- [ ] Update JSDoc comments: Refresh function documentation to reflect async nature
- [ ] Lint code: Run `npm run lint` to check code style
- [ ] Commit changes: Create commit with descriptive message
- [ ] Run integration tests: Execute `npm run test:integration` if available
- [ ] Review changes: Verify no functionality was changed, only implementation

## Notes
**Caution:**
- Do not change function signatures or return types
- Maintain backward compatibility where possible
- Ensure error handling is preserved or improved

**Benefits:**
- Improved readability
- Better error handling
- Easier debugging
- Modern JavaScript patterns

**Verification:**
- Compare before/after behavior
- Ensure all tests pass
- Manual test in development environment
```

---

## Example 4: Multi-Document Playbook

Use this pattern for complex workflows that benefit from separation into multiple documents.

### Document 1: Setup and Initialization

```markdown
# 01-Setup-Project

## Context
Initialize a new React project with TypeScript, testing, and development tooling. This document runs once to set up the foundation.

## Tasks
- [ ] Create project directory: Run `mkdir my-app && cd my-app`
- [ ] Initialize React app: Execute `npx create-react-app my-app --template typescript`
- [ ] Install dependencies: Run `npm install react-router-dom axios zustand`
- [ ] Install dev dependencies: Run `npm install -D @testing-library/react @testing-library/jest-dom @testing-library/user-event`
- [ ] Configure ESLint: Copy `.eslintrc.json` configuration from project templates
- [ ] Configure Prettier: Copy `.prettierrc` configuration from project templates
- [ ] Create .env file: Add environment variables template
- [ ] Setup folder structure: Create directories `src/components`, `src/services`, `src/utils`, `src/types`
- [ ] Initialize git: Run `git init && git add . && git commit -m "Initial setup"`
- [ ] Verify setup: Run `npm start` and confirm app loads at http://localhost:3000

## Notes
**One-Time Setup:**
This document should run once. Do not enable "Reset on Completion" for this document.

**Next Steps:**
After completion, proceed to `02-Implement-Features.md`
```

### Document 2: Implementation (Loopable)

```markdown
# 02-Implement-Features

## Context
Implement features for the application. This document can be run in loop mode as features are added incrementally.

## Tasks
- [ ] Read feature requirements: Check `docs/features/` for feature specifications
- [ ] Implement feature: Create components, services, and types as specified
- [ ] Add routing: Update `src/App.tsx` with new routes if needed
- [ ] Write unit tests: Create test files for new components and services
- [ ] Write integration tests: Create end-to-end tests if feature requires complex flow
- [ ] Run tests: Execute `npm test` to verify implementation
- [ ] Manual test: Test feature in browser
- [ ] Update documentation: Add feature documentation to `docs/`
- [ ] Code review: Check for style, performance, and best practices

## Notes
**Loop Mode:**
Enable "Reset on Completion" and loop mode for this document to process multiple features sequentially.

**Feature Pattern:**
Each iteration should focus on one feature. Read feature specs from `docs/features/<feature-name>.md`
```

### Document 3: Verification and Deployment

```markdown
# 03-Verify-and-Deploy

## Context
Final verification and deployment preparation. Run this after all features are implemented.

## Tasks
- [ ] Run full test suite: Execute `npm test` and verify all tests pass
- [ ] Run linter: Execute `npm run lint` and fix any issues
- [ ] Check bundle size: Run `npm run build` and review output size
- [ ] Test in production mode: Start production build and verify functionality
- [ ] Check console for errors: Open DevTools and verify no errors or warnings
- [ ] Verify all features: Test each documented feature for completeness
- [ ] Update CHANGELOG: Document changes in `CHANGELOG.md`
- [ ] Create release tag: Run `git tag -a v1.0.0 -m "Release version 1.0.0"`
- [ ] Push to remote: Execute `git push origin main --tags`
- [ ] Deploy to staging: Follow deployment instructions for staging environment
- [ ] Smoke test staging: Verify application works in staging
- [ ] Deploy to production: Follow deployment instructions for production
- [ ] Smoke test production: Verify application works in production
- [ ] Monitor errors: Check error tracking for any issues

## Notes
**Deployment Checklist:**
- [ ] All tests passing
- [ ] No lint errors
- [ ] Console is clean
- [ ] Bundle size is acceptable
- [ ] Staging tests passed
- [ ] Production smoke tests passed
```

---

## Example 5: Quick Task (Small Scope)

Use this pattern for quick, focused tasks.

```markdown
# Update README with Installation Instructions

## Context
The project README is missing clear installation instructions. New users struggle to set up the development environment.

## Tasks
- [ ] Read current README: Examine existing content to maintain consistency
- [ ] Add prerequisites section: List required tools (Node.js, npm, etc.)
- [ ] Add installation section: Write step-by-step setup instructions
- [ ] Add development commands: Document `npm start`, `npm test`, `npm run build`
- [ ] Add troubleshooting section: Include common issues and solutions
- [ ] Add links to documentation: Reference external docs if needed
- [ ] Verify instructions: Follow instructions on a fresh machine to confirm they work
- [ ] Update format: Ensure consistent markdown formatting with existing README
```

---

## Task Writing Patterns

### Action Verbs
Use clear, actionable verbs for task descriptions:
- **Implement**: Create new code or features
- **Update**: Modify existing code or documentation
- **Refactor**: Improve code structure without changing behavior
- **Test**: Verify functionality works correctly
- **Fix**: Resolve bugs or issues
- **Remove**: Delete unused code or files
- **Add**: Add new features, tests, or documentation
- **Configure**: Set up tools, services, or settings
- **Deploy**: Release application to environment
- **Verify**: Confirm something is correct or complete

### Context Inclusion
What context to include in task descriptions:

**Include:**
- File paths and names
- Specific values or configurations
- Expected outcomes
- How to verify completion
- Dependencies on other tasks

**Don't Include:**
- Excessive project background (put in Context section instead)
- Tutorial-style explanations
- Duplicated information from README or docs

### Verification Tasks
Always include tasks that verify work is correct:

**After implementation:**
- Run tests
- Build application
- Check for errors
- Verify output

**After changes:**
- Review changes visually
- Test in browser
- Check logs
- Confirm behavior

**Final verification:**
- Run full test suite
- Manual smoke test
- Review all changes
- Update documentation

---

## Common Anti-Patterns

### ❌ Too Vague
```markdown
- [ ] Fix authentication
```
**Better:**
```markdown
- [ ] Fix authentication bug where users can't log in with special characters in password
```

### ❌ Too Large
```markdown
- [ ] Implement entire user management system with CRUD operations, validation, error handling, and tests
```
**Better:**
```markdown
- [ ] Create user model with database schema
- [ ] Implement user CRUD operations in API
- [ ] Add input validation for user data
- [ ] Write unit tests for user API endpoints
- [ ] Write integration tests for user management
```

### ❌ Dependent on Context
```markdown
- [ ] Update the file to fix the issue
```
**Better:**
```markdown
- [ ] Update `src/components/Login.tsx` to add email validation
```

### ❌ No Verification
```markdown
- [ ] Add error handling to API
```
**Better:**
```markdown
- [ ] Add error handling to API in `src/services/api.ts`
- [ ] Test error handling by triggering API failures
```

---

## Examples Summary

| Pattern | Use When | Key Characteristics |
|---------|----------|---------------------|
| Feature Implementation | Building new features | Multiple phases, setup → implement → test |
| Bug Fix | Resolving specific issues | Root cause analysis, targeted fixes, regression testing |
| Refactoring | Improving code quality | Backward compatibility, comprehensive testing |
| Multi-Document Playbook | Complex workflows | Separation of concerns, loopable documents |
| Quick Task | Small, focused work | Single responsibility, fast execution |