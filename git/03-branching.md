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

## Branch Strategy

### Branch Roles
- **`main`**: Production-ready code only. Always stable and deployable.
- **`dev`**: Development branch where most work happens. Integration point for features.
- **Feature branches**: Created from `dev`, merged back to `dev` when complete.

## Workflow

### 1. Create Branch from Dev
```bash
git checkout dev
git pull origin dev
git checkout -b feature/your-feature-name
```

### 2. Work on Your Branch
```bash
# Make changes
git add .
git commit -m "feat(module): clear message"
git push origin feature/your-feature-name
```

### 3. Create Pull Request to Dev
Push your branch and create a PR to merge into `dev` on GitHub (see `../github/` guide).

### 4. After Review & Merge to Dev
```bash
git checkout dev
git pull origin dev
```

### 5. Release to Main (When Ready)
When a deliverable is ready for production, create a PR from `dev` to `main`:
```bash
git checkout dev
git pull origin dev
git checkout -b release/your-version
git push origin release/your-version
# Then create PR on GitHub with base branch set to main
```

## Best Practices

- **One feature per branch**: Keep scope clear
- **Pull latest dev regularly**: Avoid big conflicts later
  ```bash
  git fetch origin
  git rebase origin/dev
  ```
- **Delete branch after merge**: Clean up old branches
  ```bash
  git branch -d feature/your-feature-name
  git push origin --delete feature/your-feature-name
  ```
- **Never commit directly to main or dev**: Always use PRs for review
- **Keep main stable**: Only merge release-ready code to main

## Branch Status

```bash
git branch                    # Local branches
git branch -r                 # Remote branches
git branch -a                 # All branches
```

## Sync with Dev (if dev changed)

```bash
git fetch origin
git rebase origin/dev
# Or if rebase causes issues:
git merge origin/dev
```
