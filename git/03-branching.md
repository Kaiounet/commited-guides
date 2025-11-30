# Feature Branch Strategy

## Branch Naming Convention

Format: `<type>/<short-description>`

### Types
- `feature/` - New features
- `fix/` - Bug fixes
- `docs/` - Documentation
- `refactor/` - Code improvements
- `hotfix/` - Urgent production fixes

### Examples
- ✅ `feature/user-authentication`
- ✅ `fix/login-button-styling`
- ✅ `docs/api-endpoints`
- ❌ `my-branch`
- ❌ `update-stuff`
- ❌ `FEATURE/AUTHENTICATION` (avoid all caps)

## Workflow

### 1. Create Branch from Main
```bash
git checkout main
git pull origin main
git checkout -b feature/your-feature-name
```

### 2. Work on Your Branch
```bash
# Make changes
git add .
git commit -m "feat(module): clear message"
git push origin feature/your-feature-name
```

### 3. Create Pull Request
Push your branch and create a PR on GitHub (see `../github/` guide).

### 4. After Review & Merge
```bash
git checkout main
git pull origin main
```

## Best Practices

- **One feature per branch**: Keep scope clear
- **Pull latest main regularly**: Avoid big conflicts later
  ```bash
  git fetch origin
  git rebase origin/main
  ```
- **Delete branch after merge**: Clean up old branches
  ```bash
  git branch -d feature/your-feature-name
  git push origin --delete feature/your-feature-name
  ```
- **Never commit directly to main**: Always use PRs for review

## Branch Status

```bash
git branch                    # Local branches
git branch -r                 # Remote branches
git branch -a                 # All branches
```

## Sync with Main (if main changed)

```bash
git fetch origin
git rebase origin/main
# Or if rebase causes issues:
git merge origin/main
```
