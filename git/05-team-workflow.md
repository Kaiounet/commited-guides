# Academic Project Workflow & Best Practices

## The Complete Workflow (Day-to-Day)

### Morning: Sync with Latest Changes
```bash
git checkout dev
git pull origin dev
git checkout feature/your-feature
git rebase origin/dev  # or merge if rebasing feels risky
```

### During Work: Commit Regularly
```bash
# Check what changed
git status
git diff

# Stage your work
git add .

# Commit with meaningful message
git commit -m "feat: add user profile page"

# Push to keep backup on GitHub
git push origin feature/your-feature
```

### Before End of Day: Create/Update PR
1. Visit GitHub
2. If PR doesn't exist: Click "New pull request", set base to `dev`
3. Write clear description of what you did
4. Request review from teammates
5. Check for conflicts

### When PR is Approved: Merge
```bash
# Option 1: Merge on GitHub (recommended)
# Click "Merge pull request" on GitHub

# Option 2: Merge locally
git checkout dev
git pull origin dev
git merge feature/your-feature
git push origin dev

# Clean up
git branch -d feature/your-feature
git push origin --delete feature/your-feature
```

## Working with Your Team

### Parallel Development
Multiple people can work on different features simultaneously:

```
main ──────────────────────── (stable, production)
 │
 └─ dev ────────────────────── (integration branch)
     │
     ├─ feature/user-auth ──── (dev A)
     ├─ feature/dashboard ─── (dev B)
     └─ feature/api-endpoints (dev C)
```

**Rule**: Always create feature branches from `dev`, never from `main`.

### Code Review Expectations
- Reviews usually happen within 24 hours
- Reviewers will request changes if needed
- Address feedback promptly
- Respond to comments even if you disagree

### Handling Rejected PRs
If a reviewer requests changes:

```bash
git checkout feature/your-feature
# Make the requested changes
git add .
git commit -m "fix: address review feedback"
git push origin feature/your-feature
# Re-request review on GitHub
```

The PR updates automatically—no need to create a new one!

## Keeping Dev Stable

As a team, you're responsible for keeping `dev` working:

- **Never merge broken code** to `dev`
- **Test before requesting review** - don't waste reviewer time
- **Run tests locally** before pushing
- **Read CI/CD feedback** - if builds fail, fix it immediately

### What NOT to Do
```bash
# ❌ Never force push to dev
git push --force origin dev

# ❌ Never merge without testing
git push && sleep 1 && git merge

# ❌ Never push secrets
# (check for API keys, passwords, tokens)

# ❌ Never commit node_modules, build artifacts
# (should be in .gitignore)
```

## Release Process: Dev → Main

When your instructor/team lead says you're ready for a release:

```bash
# 1. Create release branch from dev
git checkout dev
git pull origin dev
git checkout -b release/v1.0.0

# 2. Push it
git push origin release/v1.0.0

# 3. Create PR on GitHub
# - Base: main
# - Compare: release/v1.0.0
# - Title: "Release v1.0.0: Brief description"

# 4. Get approval and merge
# 5. Tag the release
git checkout main
git pull origin main
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin v1.0.0

# 6. Clean up
git branch -d release/v1.0.0
git push origin --delete release/v1.0.0
```

## Documentation in Git

### README.md
- **What**: Project overview and setup instructions
- **Who updates**: Everyone when adding new sections
- **Location**: Root of repository

### CONTRIBUTING.md
- **What**: How to contribute to the project
- **Who updates**: Tech lead
- **Includes**: Branching strategy, testing requirements, PR process

### CHANGELOG.md
- **What**: Record of what changed in each version
- **Who updates**: During release
- **Format**: One entry per release with features, fixes, breaking changes

Example:
```markdown
## [1.0.0] - 2025-11-30
### Added
- User authentication system
- Dashboard with data visualization

### Fixed
- Login form validation bug
- Mobile responsive design

### Changed
- Database schema for users table
```

## Troubleshooting Common Issues

### "Your branch is ahead of origin/dev"
```bash
# You have local commits not pushed yet
git push origin feature/your-feature
```

### "Your branch is behind origin/dev"
```bash
# You need to pull latest changes
git pull origin feature/your-feature
```

### "Untracked files will be overwritten"
```bash
# Clean up first
git clean -fd
# Then pull
git pull origin dev
```

### Everyone sees conflicts in the same file
- This means your team needs to coordinate
- Discuss in Scrum standup
- One person fixes the file, others pull after merge

## Quick Checklist Before Pushing

- [ ] Did I pull latest `dev` first?
- [ ] Are my changes related to my task?
- [ ] Did I test locally?
- [ ] Did I follow commit message standards?
- [ ] Did I remove debug code/console.logs?
- [ ] Did I check for accidental file deletions?
- [ ] Would another developer understand these changes?
