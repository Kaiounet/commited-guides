# Quick Reference & Cheat Sheet

## Daily Commands Cheat Sheet

### Morning Routine
```bash
git checkout dev              # Switch to dev
git pull origin dev           # Get latest
git checkout feature/task     # Switch to your branch
git rebase origin/dev         # Stay up to date
```

### During Work
```bash
git status                    # What changed?
git diff                      # See my changes
git add .                     # Stage all
git commit -m "feat: clear message"  # Save work
git push origin feature/task  # Back up to GitHub
```

### Before Lunch/End of Day
```bash
git log -1                    # Verify commit
git push origin feature/task  # Ensure backed up
# Create/update PR on GitHub
```

### Before Leaving
```bash
git status                    # Should be clean
git log --oneline -5          # See recent work
# Check PR has description
# Team lead will review overnight
```

## Branch Quick Commands

```bash
# Create and switch to new branch
git checkout -b feature/my-feature

# List all branches
git branch -a

# Delete local branch
git branch -d feature/my-feature

# Delete remote branch
git push origin --delete feature/my-feature

# See which branch I'm on
git status

# Switch between branches
git checkout feature/other
git checkout dev

# See what's ahead/behind
git status
```

## Commit Message Quick Guide

```
Format: <type>(<scope>): <message>

Examples:
feat(auth): add JWT token generation
fix(api): handle null responses
docs(readme): update setup instructions
refactor(db): optimize query performance
test(user): add login validation tests
```

## PR Checklist (Before Requesting Review)

```
[ ] Pulled latest dev
[ ] Code follows style guide
[ ] Tests pass locally
[ ] No console.logs left
[ ] No hardcoded secrets
[ ] PR title is descriptive
[ ] PR description explains what/why
[ ] Linked related issue(s)
[ ] One reviewer assigned
```

## PR Review Checklist (As Reviewer)

```
[ ] Read the description
[ ] Understand the goal
[ ] Review the code
[ ] Check for bugs
[ ] Verify tests exist
[ ] See if it's well-documented
[ ] Approve or request changes
[ ] Leave constructive feedback
```

## Merge Conflict Resolution

```bash
# See conflict markers
git status
cat file-with-conflict.js

# Markers look like:
# <<<<<<< HEAD
# your changes
# =======
# their changes
# >>>>>>>

# Resolve manually in editor, then:
git add .
git commit -m "fix: resolve merge conflict"
git push origin feature/your-feature
```

## Common Scenarios

### "I need to switch branches but have uncommitted changes"
```bash
git stash               # Save changes
git checkout other-branch
git checkout previous-branch
git stash pop           # Restore changes
```

### "I committed to wrong branch"
```bash
git reset HEAD~1        # Undo commit, keep changes
git stash               # Save the changes
git checkout correct-branch
git stash pop           # Restore changes
git commit -m "msg"
git push
```

### "I made a typo in my commit message"
```bash
git commit --amend -m "new message"
git push --force-with-lease origin feature/branch
```

### "I want to see what changed between branches"
```bash
git diff dev..feature/my-feature
```

### "I need to sync with latest dev"
```bash
git fetch origin
git rebase origin/dev   # Or merge if unsure
```

## Scrum Quick Reference

### Sprint Planning (What? How much?)
```
Input: Backlog of features
Output: Sprint backlog with story points
Time: 1-2 hours
Product Owner: Explains features
Team: Estimates effort (1, 2, 3, 5, 8, 13 points)
Result: Sprint commitment
```

### Daily Standup (What? What's next? Blocked?)
```
Time: 10 minutes
Question 1: What did you do yesterday?
Question 2: What will you do today?
Question 3: Are you blocked?
Format: Each person ~2 minutes
```

### Sprint Review (Did we finish it?)
```
Input: Completed work
Output: Accepted or rejected items
Time: 1 hour
Activity: Demo features to Product Owner
Feedback: Customer/instructor approval
```

### Sprint Retrospective (What to improve?)
```
Input: Sprint experience
Output: Improvements for next sprint
Time: 45 minutes
Format:
  - What went well (10 min)
  - What didn't (10 min)
  - Action items (20 min)
  - Assign owners (5 min)
```

## Estimation Guide

| Points | Effort | Examples |
|--------|--------|----------|
| 1 | Trivial | Fix typo, add comment, simple constant |
| 2 | Easy | Change variable name, add validation |
| 3 | Small | Simple function, basic endpoint |
| 5 | Medium | Feature with tests, form with validation |
| 8 | Large | Complex feature, multiple endpoints |
| 13 | Very Large | Big feature, needs multiple PRs |

**If it's > 13 points, break it down into smaller stories.**

## Team Velocity Tracking

```
Sprint 1: 24 points completed ✓
Sprint 2: 20 points completed ✓
Sprint 3: 26 points completed ✓
Average: 23 points/sprint

Plan future sprints at ~23 points
```

## Communication Channels

| Channel | Use For | Response Time |
|---------|---------|----------------|
| Standup | Daily sync | N/A (scheduled) |
| GitHub Issues | Tasks, bugs, features | 48 hours |
| PR Comments | Code feedback | 24 hours |
| Slack | Questions, quick help | 1-2 hours |
| Retro Notes | Lessons learned | N/A (documented) |

## Red Flags 🚩

- ❌ Not committing for days
- ❌ PR with no description
- ❌ Someone hasn't spoken in standup
- ❌ Tests failing but merged anyway
- ❌ Secrets in code
- ❌ No communication about blockers
- ❌ Major conflicts in same file (coordination issue)

## When You're Stuck

**Step 1**: Check if the error message is clear
```bash
# Read the full error
npm run dev    # See the actual problem
```

**Step 2**: Google the error (seriously, everyone does)

**Step 3**: Check documentation
- README
- Architecture docs
- Similar code in project

**Step 4**: Ask on Slack with context
```
"Getting error XYZ when running tests.
Already tried ABC.
Relevant file: src/auth.js
```

**Step 5**: Pair with teammate if stuck >30 min
```
"Hey, help me debug this? 
Available in 10 min?"
```

**Step 6**: Tell standup you're blocked
```
"I'm blocked on DB schema for auth task.
Need help from Morgan."
```

## Quick File Templates

### PR Description
```markdown
## Description
Brief explanation of what this does.

## Why?
Problem this solves or feature this adds.

## Changes
- Added X
- Updated Y

## Testing
How to test:
1. Step 1
2. Step 2

## Related Issues
Closes #123
```

### Issue Template
```markdown
## Description
What's the problem or feature?

## Acceptance Criteria
- Criterion 1
- Criterion 2

## Related Work
Any related issues?
```

### Commit Message
```
feat(module): add new feature
fix(component): resolve styling issue
docs(readme): update installation steps
```

## Resources

- **Git**: `../git/` guides
- **GitHub**: `../github/` guides
- **Scrum**: `../scrum/` guides
- **Docs**: `../typst/` guides
- **Team**: Ask in standup!
