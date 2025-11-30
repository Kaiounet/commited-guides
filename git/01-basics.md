# Git Basics for Your Project

## Initial Setup

### Configure Your Identity
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@university.edu"
```

### Clone the Repository
```bash
git clone <repo-url>
cd <project-name>
```

## Basic Workflow

### 1. Check Status
```bash
git status
```
Shows modified files, staged changes, and branch info.

### 2. Make Changes
Edit files in your editor as normal.

### 3. Stage Changes
```bash
git add .                    # Stage all changes
git add src/file.js          # Stage specific file
git add src/                 # Stage entire directory
```

### 4. Commit
```bash
git commit -m "Clear message describing what changed"
```

### 5. Push to Remote
```bash
git push origin <branch-name>
```

### 6. Pull Latest Changes
```bash
git pull origin main
```

## Check Your Work

```bash
git log --oneline -10        # View last 10 commits
git diff                     # See unstaged changes
git diff --staged            # See staged changes
```

## Undo Mistakes

```bash
git restore file.js          # Undo changes to file (not staged)
git restore --staged file.js # Unstage file
git reset HEAD~1             # Undo last commit, keep changes
```

## Quick Reference

| Command | Purpose |
|---------|---------|
| `git status` | Check current state |
| `git add .` | Stage all changes |
| `git commit -m "msg"` | Save changes |
| `git push` | Upload commits |
| `git pull` | Download updates |
| `git log` | View history |
