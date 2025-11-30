# Commit Standards for Team Collaboration

## Commit Message Format

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Type
Must be one of:
- `feat`: A new feature
- `fix`: A bug fix
- `docs`: Documentation changes
- `style`: Code style (formatting, semicolons)
- `refactor`: Code restructuring (no behavior change)
- `perf`: Performance improvements
- `test`: Adding or updating tests
- `chore`: Dependencies, build config, etc.

### Scope (optional)
The area affected: `auth`, `ui`, `database`, `api`

### Subject
- Max **50 characters**
- Imperative mood: "add" not "adds" or "added"
- No period at end

### Body (optional)
- Max **72 characters** per line
- Explain WHAT and WHY, not HOW
- Leave blank line after subject

### Footer (optional)
Reference issues: `Closes #123` or `Fixes #456`

## Examples

### Good Commits
```
feat(auth): add email verification on signup

Users can now verify their email address during signup.
This prevents spam accounts and enables password recovery.

Closes #42
```

```
fix(api): handle missing user gracefully

Returns 404 with descriptive error message instead of
crashing server.

Fixes #89
```

```
docs: update README with setup instructions
```

### Avoid These
- ❌ "fixes stuff"
- ❌ "updated code"
- ❌ "Work in progress - DO NOT MERGE"
- ❌ Commit messages longer than 50 chars for subject

## Length Guidelines

- **1-2 commits per task**: Don't create one commit per line
- **Atomic commits**: Each commit is a complete logical unit
- **When in doubt**: One commit is better than many small ones

## Before Pushing

```bash
git log --oneline -5  # Review your commits
git diff origin/main  # Check what you're about to push
```
