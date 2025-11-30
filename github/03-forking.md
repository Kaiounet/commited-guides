# Forking for External Contributors

## When to Fork

You fork a repository when:
- You don't have write access
- You want to contribute to open-source projects
- You want a personal copy to experiment with

**For team members with repository access**, you don't need to fork - use branches instead (see `01-collaboration-basics.md`).

## Forking Workflow

### Step 1: Fork the Repository
1. Go to the original GitHub repository
2. Click the "Fork" button (top right)
3. Select your GitHub account as the destination

This creates your own copy of the repository under your account.

### Step 2: Clone Your Fork
```bash
git clone https://github.com/YOUR-USERNAME/project-name.git
cd project-name
```

### Step 3: Add Upstream Remote
This keeps your fork synced with the original:

```bash
git remote add upstream https://github.com/ORIGINAL-OWNER/project-name.git
git remote -v  # Verify you have two remotes: origin and upstream
```

### Step 4: Create a Feature Branch
```bash
git checkout -b feature/your-feature
# Make changes, commit, push
git push origin feature/your-feature
```

### Step 5: Create a Pull Request
1. Go to your fork on GitHub
2. Click "New pull request"
3. Set base repository to `ORIGINAL-OWNER/project-name` (main branch)
4. Set compare to `YOUR-USERNAME/project-name` (your feature branch)
5. Fill out PR template and submit

## Keeping Your Fork Updated

### Sync with Upstream
```bash
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
```

### Or Rebase on Upstream
```bash
git fetch upstream
git rebase upstream/main
git push origin main --force-with-lease
```

## Tips

- **Always fetch upstream before starting**: Avoid conflicts
- **Create feature branches**: Don't work on main
- **Keep commits clean**: See `../git/02-commit-standards.md`
- **Check for existing PRs**: Don't duplicate work
