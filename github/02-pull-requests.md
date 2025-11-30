# Pull Requests: The Code Review Process

## What is a Pull Request?

A PR is how you propose changes to the project. It allows teammates to review, discuss, and approve your code before merging.

## Creating a Pull Request

### Step 1: Push Your Branch
```bash
git push origin feature/your-feature-name
```

### Step 2: Open PR on GitHub
1. Go to the repository on GitHub.com
2. Click "Pull requests" tab
3. Click "New pull request"
4. Select your branch as "compare" branch
5. **`dev` should be "base" branch** (for feature PRs)

### Step 3: Write Your PR Description

Use this template:

```markdown
## Description
Brief explanation of what this PR does.

## Why?
Explain the problem this solves or feature this adds.

## Changes
- Added user authentication
- Updated login form styling
- Added email verification

## Testing
How to test this locally:
1. Run `npm install`
2. Run `npm run dev`
3. Navigate to /login
4. Enter test credentials

## Related Issues
Closes #123
```

### Step 4: Request Review
1. In the PR, find "Reviewers" on the right
2. Select team members to review

## Reviewing a Pull Request

### As a Reviewer

1. **Read the description** - Understand the intent
2. **Review the changes**
   - Click "Files changed"
   - Read through each change
3. **Comment on code**
   - Hover over a line
   - Click "+" to add a comment
4. **Approve or Request Changes**
   - Click "Review changes"
   - Choose "Approve" or "Request changes"

### Comments

```
// Specific feedback on a line
This could use a null check before accessing property.

// General questions
Why are we using this library instead of the built-in option?
```

## Responding to Feedback

1. **Read comments** - Understand what needs changing
2. **Make changes** in your local branch
3. **Commit and push**
   ```bash
   git add .
   git commit -m "fix: address review feedback"
   git push origin feature/your-feature-name
   ```
4. **Respond to comments** - Mark as resolved or explain decisions

## Merging

1. **Wait for approvals** - At least one review (check team guidelines)
2. **Resolve conflicts** (if any appear)
3. **Click "Merge pull request"**
4. **Delete branch** - Cleanup after merging

### Merging to Main (Release)

When a feature set is ready for production, create a PR from `dev` to `main`:

1. Click "New pull request"
2. Set **`main`** as base branch and **`dev`** (or a release branch) as compare
3. Write a release description including all changes and improvements
4. Request review from the team lead
5. Merge to main once approved
6. Follow team release procedures (deployment, tagging, etc.)

## Best Practices

- **Keep PRs focused**: One feature per PR
- **Small PRs merge faster**: Easier to review
- **Descriptive titles**: "Add user authentication" not "Updates"
- **Be respectful**: Reviews are about code, not people
- **Respond promptly**: Keep momentum going
- **Test before requesting review**: Don't waste reviewer time

## Common Issues

### Merge Conflicts
If dev has changed since you started:
```bash
git fetch origin
git rebase origin/dev
# Resolve conflicts in your editor
git add .
git rebase --continue
git push origin feature/your-feature-name --force-with-lease
```

### PR Won't Merge (Branch Out of Date)
GitHub will show a "Update branch" button. Click it, or:
```bash
git checkout feature/your-feature
git fetch origin
git merge origin/dev
git push origin feature/your-feature
```
