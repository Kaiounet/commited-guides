# Project Structure & Standards

## Repository Organization

Your project should be organized to make it easy for everyone to find things and understand the structure.

### What We're Building

A [project description] with [key components]. This guide helps you understand the project structure and standards we follow.

### Code Organization

- **Clear structure** - Anyone should understand the layout without asking
- **Consistent naming** - Files, folders, functions follow same patterns
- **Documentation** - Code directories have README explaining purpose
- **Separation of concerns** - Frontend, backend, tests cleanly separated

### Definition of Done (Per Feature)

Before you consider work "done", verify:
- ✅ Code written and tested
- ✅ PR reviewed and approved
- ✅ Merged to dev
- ✅ Tests passing in CI/CD
- ✅ No regressions in other features
- ✅ Documentation updated
- ✅ Team understands what you built

## Standards We Follow

### Code Quality Standards

**General Rules**
- Clean, readable code is non-negotiable
- Follow the project's code style (check CONTRIBUTING.md)
- No debug code, console.logs, or commented-out code in PRs
- No secrets (passwords, API keys, tokens) in commits

**Testing**
- Write tests for new features
- Tests must pass before PR is created
- Target 60%+ code coverage
- Critical paths (auth, payments, etc.) should have tests

**Documentation**
- README explains how to setup and run the project
- API endpoints documented with examples
- Complex logic has comments explaining why (not what)
- Architecture documented for future developers

### Our Git Workflow

See `/git/03-branching.md` for complete guide. Quick version:

1. **Create feature branch from dev**
   ```bash
   git checkout dev
   git pull origin dev
   git checkout -b feature/your-feature
   ```

2. **Work on your branch**
   - Make small, focused commits
   - Follow commit standards (`../git/02-commit-standards.md`)
   - Push regularly to have backup

3. **Create PR when ready**
   - Write clear description
   - Link to related issue
   - Ensure tests pass locally
   - Request review from teammate

4. **Address feedback**
   - Read reviewer comments
   - Make requested changes
   - Push again (PR updates automatically)
   - Respond to comments

5. **Merge when approved**
   - Click "Merge pull request" on GitHub
   - Delete branch after merge
   - Celebrate!

### Code Review Process

**You'll review others' code too.** Here's what to look for:

1. **Understand the goal** - Read PR description first
2. **Does it solve the problem?** - Check if it matches the issue/request
3. **Is the code quality good?** - Readable? Well-structured?
4. **Are there bugs?** - Look for obvious issues
5. **Are tests there?** - New features should have tests
6. **Leave feedback** - Be constructive, not harsh
7. **Approve or request changes** - Your call

**Example good review comment:**
```
This function is doing two things. Could you split it into 
`validateEmail()` and `sendVerification()`? Would be easier to test.

Also, what happens if the email is already verified? Should we 
return a different status?
```

**Example bad review comment:**
```
This is bad code.
```

### Repository Structure

```
project-name/
├─ README.md              (Setup instructions, project overview)
├─ CONTRIBUTING.md        (How we develop, our standards)
├─ src/                   (Source code)
│  ├─ frontend/
│  ├─ backend/
│  └─ shared/
├─ tests/                 (Test files)
├─ docs/
│  ├─ architecture.md
│  ├─ api.md
│  └─ database.md
├─ package.json           (Dependencies)
└─ .gitignore            (What NOT to commit)
```

### Branch Protection Rules

We have rules on GitHub to keep code quality high:

**On `dev` and `main` branches:**
- ✅ Require PR review (1+ approval)
- ✅ Require status checks pass (tests, linting)
- ✅ Require branch up to date
- ✅ No force pushing

**What this means for you:**
- You can't merge your own PR
- You can't bypass failing tests
- You must get another person to approve
- Keeps us honest

## Issues & Task Management

### Creating an Issue

When you find a bug or want to implement a feature:

1. Click "Issues" on GitHub
2. Click "New issue"
3. Use a clear title: `[TYPE] Brief description`
4. Explain what needs to be done
5. Add labels (bug, feature, help-wanted, etc.)
6. Add story points if known

**Example Issue:**
```
Title: [FEATURE] Add password reset email

Description:
Users should be able to reset their password via email link.

Acceptance Criteria:
- User clicks "Forgot Password"
- Enters email address
- Receives email with reset link (valid 24 hours)
- Clicks link and can set new password
- Old password no longer works

Related: 
Blocks: Feature X (depends on this)
```

### Assigning Work

- Assign yourself when you start work
- Move to "In Progress" on project board
- Create a branch for it
- Link your PR to the issue: "Closes #42"
- When merged, issue closes automatically

## Testing & Quality

### Writing Tests

You don't need 100% coverage, but critical features need tests:

- **Authentication** - Test login/logout/permissions
- **Forms** - Test validation
- **APIs** - Test endpoints
- **Calculations** - Test complex logic

**Tests help because:**
- Catch bugs before production
- Prevent regressions
- Document how code should work
- Give confidence to reviewers
- Make refactoring safe

### Running Tests

```bash
npm run test              # Run all tests
npm run test:watch       # Watch mode
npm run test:coverage    # See coverage report
```

## Documentation Standards

### README.md

Your project README should have:

```markdown
# Project Name

Brief description (what is this, why does it exist)

## Quick Start

```bash
npm install
npm run dev
```

## Features

- Feature 1
- Feature 2

## Project Structure

Explain folder layout

## Contributing

See CONTRIBUTING.md

## Tech Stack

- Frontend: React
- Backend: Node.js
- Database: PostgreSQL
```

### API Documentation

When you add an endpoint, document it:

```
## POST /api/users/login

Authenticate user with email and password.

**Request:**
```json
{
  "email": "user@example.com",
  "password": "secret123"
}
```

**Response (200):**
```json
{
  "token": "eyJhbG...",
  "user": {
    "id": "123",
    "email": "user@example.com"
  }
}
```

**Errors:**
- 400: Missing email or password
- 401: Invalid credentials
- 500: Server error
```

### Architecture Documentation

Create `docs/architecture.md`:

```markdown
# Architecture

## Overview

High-level diagram of system

## Frontend

- React with hooks
- Redux for state
- Tailwind for styling

## Backend

- Express.js server
- JWT authentication
- PostgreSQL database

## Key Decisions

Why we chose these technologies and how they work together
```

## Sprint Commitments

### Per Sprint (1 week)

**What you commit to:**
- Estimated story points (realistic, not wishful)
- Specific features/fixes
- Definition of done met

**What "done" means:**
- Code written
- Tests passing
- Reviewed and approved
- Merged to dev
- Works without breaking other features
- Documented

### Velocity Tracking

We track how many points you complete each sprint:

```
Sprint 1: 24 points ✓
Sprint 2: 26 points ✓
Sprint 3: 20 points (slow week, but honest)
Average: ~23 points/sprint
```

This helps plan realistic future sprints.

## Sprint Events (Our Rhythm)

### Sprint Planning

**When:** Monday morning (1.5-2 hours)

What happens:
1. Look at backlog of issues
2. Team estimates effort (story points)
3. Commit to what we'll do this sprint
4. Assign issues to people
5. Define sprint goal

### Daily Standup

**When:** 10 minutes, every morning

You share:
1. What did you do yesterday?
2. What will you do today?
3. Are you blocked? What's blocking you?

**This keeps team aligned.** If you're stuck, we help immediately.

### Sprint Review (Demo)

**When:** Friday afternoon (1 hour)

What happens:
1. Demo the features you built
2. Get feedback
3. Celebrate wins

### Sprint Retrospective (Improve)

**When:** Friday afternoon (45 min, after review)

You discuss:
1. What went well?
2. What didn't?
3. What will we improve next sprint?

## Common Patterns & Anti-Patterns

### ✅ Good Practices

- Commit regularly (not once at end of day)
- Push daily (have backup on GitHub)
- Small PRs (easier to review)
- Clear PR descriptions (why you did it)
- Ask for help early (before stuck 2+ hours)
- Review others' code promptly (help team move)
- Celebrate merged features (morale matters)

### ❌ Avoid

- Working for days without pushing
- Giant PRs (hard to review)
- Merging without tests
- Ignoring feedback
- Silent blockers (tell team in standup!)
- Committing secrets or debug code
- Force pushing to dev/main

## When You're Stuck

**If you hit a problem:**

1. **Check the error carefully** - Read full error message
2. **Search existing code** - Similar problems solved elsewhere?
3. **Check documentation** - In `/docs` or README
4. **Ask on Slack** - Include error and what you tried
5. **Pair with teammate** - If stuck >30 minutes
6. **Tell standup** - "I'm blocked on X, need help"

**Never:**
- Silently struggle for hours
- Commit broken code hoping to fix later
- Work around the problem instead of solving it

## Your First Week

1. **Day 1**: Clone repo, read README and CONTRIBUTING.md
2. **Day 2**: Setup dev environment, run tests
3. **Day 3**: Make small fix (documentation, typo, etc.) and PR
4. **Day 4**: Get PR reviewed, make changes if requested
5. **Day 5**: PR merged, pick next issue

By end of week: You'll have merged your first PR and understand the workflow.
