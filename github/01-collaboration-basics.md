# GitHub Collaboration for Teams

## Repository Access

### Getting Access
1. Ask the tech lead/project owner to add you as a collaborator
2. Check your email for the invitation
3. Accept the invitation on GitHub

**You should now have write access to the repository!**
- You can push branches directly (no forking needed)
- You can create pull requests
- You can review teammates' code

## Your First Day

### 1. Clone the Repository
```bash
git clone <repository-url>
cd <project-name>
```

### 2. Create Your Service-Specific Branch from Dev

For CommitEd (microservices), include the service name:

```bash
git checkout dev
git pull origin dev
git checkout -b feature/auth/two-factor-authentication
# or
git checkout -b feature/user/profile-image-upload
```

**Format:** `feature/<service>/<description>`

**Available services:** `auth`, `user`, `project`, `notif`, `api`

See `../git/06-microservices-workflow.md` for full microservices workflow.

### 3. Make Your Changes
- Edit files
- Test locally
- Commit with clear messages (see `../git/02-commit-standards.md`)

### 4. Push Your Branch
```bash
git push origin feature/your-feature
```

### 5. Create a Pull Request

On GitHub.com, you'll see a suggestion to create a PR. Click it!

**Important for CommitEd:**
- Base branch should be `dev` (not main)
- Your branch should be `feature/<service>/<description>`
- Fill out PR description (see `02-pull-requests.md`)

See `02-pull-requests.md` for detailed PR workflow.

## Important: Branch Protection Rules

CommitEd has branch protection rules to maintain code quality:

**On `dev` and `main` branches:**
- ✅ You CANNOT push directly
- ✅ You MUST create a Pull Request
- ✅ At least 1 review approval required before merging
- ✅ All tests must pass
- ✅ Branch must be up-to-date with main/dev

**What this means for you:**
1. Create your feature branch (e.g., `feature/user/avatar`)
2. Make changes and push to your branch
3. Create a PR on GitHub
4. Ask a teammate to review
5. Once approved, merge the PR

This prevents broken code from reaching dev/main.

## Communication

- **Issues**: Report bugs or request features
- **Discussions**: Ask questions or brainstorm
- **PR Comments**: Review code and suggest improvements
- **GitHub Notifications**: Stay updated on changes

## Useful Links

- **GitHub Docs**: https://docs.github.com/en
- **Your Repository**: Check the README for project-specific info
