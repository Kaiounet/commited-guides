# GitHub for Academic Projects

## Issue Management

### Creating Issues

Issues are tickets for features, bugs, and tasks. Create one for anything you need to track.

**Format**: `[TYPE] Brief description`

Types:
- `[FEATURE]` - New functionality
- `[BUG]` - Something broken
- `[TASK]` - General work item
- `[DOC]` - Documentation
- `[REFACTOR]` - Code improvement

**Example**:
```
Title: [FEATURE] Add user authentication

Description:
Users should be able to sign up and log in with email/password.

Acceptance Criteria:
- Users can create account with email
- Users can log in with credentials
- Passwords are hashed and stored securely
- Invalid logins show error message

Related PR: (none yet)
```

### Issue Labels

Use labels to organize work:
- `bug` - Something's broken
- `enhancement` - New feature
- `documentation` - Docs only
- `help-wanted` - You need assistance
- `in-progress` - Someone's working on it
- `blocked` - Waiting on something else
- `high-priority` - Do this first
- `good-first-issue` - Good for new team members

### Assigning Issues

```
Assign to: [Your Name]
```

This tells the team you're working on it. Update the issue when you start, and link your PR when you're done.

## Pull Request Etiquette

### For Authors (People Making Changes)

**Before requesting review:**
- [ ] PR title is descriptive and starts with type (`feat:`, `fix:`, etc.)
- [ ] Description explains what and why
- [ ] All tests pass locally
- [ ] No debug code or console.logs
- [ ] Code follows project style
- [ ] At least one related issue is linked

**Example PR Description:**
```markdown
## Description
Implements user authentication with JWT tokens.

## Why?
Users need to log in to access the platform. This is a foundational feature.

## Changes
- Added login/signup endpoints
- Created JWT token generation
- Added password hashing with bcrypt
- Created user model in database
- Added authentication middleware

## Testing
1. Run `npm run test -- auth.test.js`
2. Signup at /signup
3. Login at /login
4. Verify token stored in localStorage

## Issues
Closes #42

## Notes
- Uses JWT for stateless auth
- Tokens expire after 7 days
- Password requirements: 8+ chars, 1 uppercase, 1 number
```

### For Reviewers (People Checking Changes)

**Read the PR description first** - It tells you what to look for.

**Check these things:**
1. Does the code solve the stated problem?
2. Does it follow the commit standards?
3. Are there obvious bugs or issues?
4. Is the code readable and well-structured?
5. Are there tests?
6. Does it break anything else?

**Leave helpful comments:**
```
// Specific issue on a line
This variable name is confusing. What does "idx" stand for? 
Consider: userId or emailIndex?

// General question
Why are we storing this in localStorage instead of sessionStorage?

// Praise (yes, do this!)
Nice refactoring here - much cleaner than before.
```

**Don't be harsh:**
- ❌ "This is terrible code"
- ✅ "Could this be clearer if we broke it into smaller functions?"

**Approve or Request Changes:**
- ✅ **Approve**: Code is ready to merge
- 🔄 **Request Changes**: Need fixes before merging
- 💭 **Comment**: Questions or suggestions (doesn't block merge)

## Collaboration Scenarios

### Scenario: Your PR has conflicts

GitHub shows: "This branch has conflicts that must be resolved"

**Fix it:**
```bash
git checkout feature/your-feature
git fetch origin
git merge origin/dev
# Resolve conflicts in your editor
git add .
git commit -m "fix: resolve merge conflicts"
git push origin feature/your-feature
```

### Scenario: Someone needs your PR feedback

When tagged or assigned as reviewer:
1. Read the description first
2. Look at changed files
3. Leave comments on specific lines
4. Choose: Approve, Request Changes, or Comment
5. Notify them on Slack/Discord

### Scenario: Your PR gets stale

If `dev` has many new commits and your PR is behind:

**GitHub shows a "Update branch" button** - Click it!

Or locally:
```bash
git checkout feature/your-feature
git fetch origin
git merge origin/dev
git push origin feature/your-feature
```

### Scenario: Multiple people need to work on same feature

If the feature is complex:
1. **First person**: Creates branch `feature/big-task`
2. **Second person**: Branches from there: `feature/big-task/sub-feature`
3. **When done**: PR back to `feature/big-task`
4. **Final**: `feature/big-task` PR to `dev`

## GitHub Teams & Permissions

### Repository Access Levels
- **Owner**: Full control (usually instructor)
- **Maintainer**: Can merge PRs, manage branches (senior devs)
- **Developer**: Can commit and PR (most students)
- **Read-only**: Can read but not commit (observers)

### Branch Protection

The `main` and `dev` branches should be protected:
- ✅ Require PR reviews before merging
- ✅ Require status checks to pass
- ✅ Require branches to be up to date
- ❌ No force pushing

**This keeps the repo stable and prevents accidents.**

## Project Boards (Optional but Useful)

Create a GitHub Project to visualize progress:

```
📋 Project: Semester Project

Todo          In Progress    In Review      Done
├─ Auth       ├─ Dashboard   ├─ Login UI    ├─ Setup
├─ Database   └─ API         └─ Logout      ├─ CI/CD
└─ Docs
```

Drag issues/PRs across as they progress. Helps the team see what everyone's working on.

## Tips for Success

- **Link issues to PRs**: Type `Closes #42` to auto-close when merged
- **Use issue templates**: Standardizes bug reports and feature requests
- **Review regularly**: Don't let PRs pile up
- **Communicate**: Use PR comments, don't have separate conversations
- **Tag teammates**: Use `@username` to notify them
- **Keep PRs small**: Easier to review, easier to revert if needed
- **Document decisions**: Explain why, not just what

## Red Flags (Don't Do This)

- ❌ PR with 50+ file changes - break it up
- ❌ PR with no description - reviewers won't know what you did
- ❌ Approving without reading the code
- ❌ Merging without tests passing
- ❌ Ignoring review comments
- ❌ Force pushing to shared branches
- ❌ Committing secrets (passwords, API keys)
