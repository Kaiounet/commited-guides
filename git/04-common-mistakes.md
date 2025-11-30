# Common Git Mistakes & Recovery

## Before You Panic

Most mistakes can be undone. **Don't delete anything important without understanding it first.**

## Mistake: Committed to Wrong Branch

### Scenario
You committed to `dev` when you meant to commit to `feature/my-task`.

### Recovery
```bash
# 1. Create your feature branch (points to current commit)
git branch feature/my-task

# 2. Reset dev to where it was before
git reset origin/dev --hard

# 3. Switch to your feature branch
git checkout feature/my-task

# 4. Push both branches
git push origin dev
git push origin feature/my-task
```

## Mistake: Made Changes Without Committing

### Scenario
You edited files but forgot to commit before switching branches.

### Recovery
```bash
# Save your work
git stash

# Switch to correct branch
git checkout feature/your-feature

# Restore your work
git stash pop
```

## Mistake: Committed Sensitive Information

### Scenario
You accidentally committed a password, API key, or `.env` file.

### ⚠️ IMMEDIATE ACTION REQUIRED
```bash
# DO NOT push if you haven't yet
# If you haven't pushed, just undo the commit:
git reset HEAD~1

# Remove the file and recommit
rm filename-with-secret
git add .
git commit -m "fix: remove sensitive file"
git push
```

**If already pushed**: Notify your team lead immediately. The secret should be rotated.

## Mistake: Merged Wrong Branch

### Scenario
You merged `feature/x` into `main` when it should go to `dev` first.

### Recovery
```bash
# Check what was merged
git log --oneline -5

# Revert the merge commit
git revert -m 1 <commit-hash>

# Or completely reset main (if not pushed)
git reset origin/main --hard
```

## Mistake: Deleted Important Branch

### Scenario
You deleted a branch with `git branch -D feature/important`.

### Recovery
```bash
# Find deleted branch
git reflog

# Recreate it from the reflog
git checkout -b feature/important <commit-hash-from-reflog>

# Push it back
git push origin feature/important
```

## Mistake: Merge Conflicts Won't Resolve

### Scenario
You have conflicts in a merge and can't figure out how to fix them.

### Recovery
```bash
# Option 1: Abort and try again
git merge --abort

# Option 2: Take theirs (dev version)
git checkout --theirs .
git add .
git commit -m "fix: resolve conflicts"

# Option 3: Take ours (your feature version)
git checkout --ours .
git add .
git commit -m "fix: resolve conflicts"
```

**Better solution**: Ask a teammate for help before committing the wrong resolution.

## Mistake: Lost Commits After Reset

### Scenario
You did `git reset --hard` and lost commits.

### Recovery
```bash
# View all recent activity
git reflog

# Recover the commit
git reset --hard <commit-hash>
```

## Mistake: Accidentally Stashed and Forgot

### Scenario
You ran `git stash` and can't remember where your changes are.

### Recovery
```bash
# List all stashes
git stash list

# View what's in a stash
git stash show -p stash@{0}

# Restore it
git stash pop stash@{0}

# Or if you want to keep the stash
git stash apply stash@{0}
```

## Best Practices to Avoid Problems

- **Never force push to shared branches** (`dev`, `main`)
  ```bash
  # ❌ NEVER
  git push --force origin dev
  
  # ✅ Use force-with-lease (safer)
  git push --force-with-lease origin feature/your-feature
  ```

- **Always pull before pushing**
  ```bash
  git pull origin <branch>
  git push origin <branch>
  ```

- **Commit often** - Small commits are easier to undo

- **Never commit directly to `dev` or `main`** - Always use PRs

- **Review your changes before committing**
  ```bash
  git diff                 # See what you changed
  git add -p              # Stage changes interactively
  ```

## Getting Help

If you're stuck:
1. Run `git status` to see current state
2. Check `git log --oneline` to see recent commits
3. Ask a team member before doing `--hard` resets
4. Use `git reflog` if you think something's lost

Remember: **Your team lead can help recover almost anything!**
