# Semantic Versioning

## What is Semantic Versioning?

A version number tells you what changed. Instead of random version numbers, we use a standard format so everyone understands the impact.

**Format: `MAJOR.MINOR.PATCH`**

Examples:
- `1.0.0` - First release
- `1.2.3` - Second minor release, third patch
- `2.0.0` - Major breaking change

## When to Version

You version your code when you **release it to production** (merge to `main`).

### PATCH (Bug fixes) - `1.0.X`
- Fixed a bug but didn't change the API
- No new features
- Everything still works the same way

**Examples:**
- `1.0.0` → `1.0.1` - Fixed login timeout bug
- `1.0.1` → `1.0.2` - Fixed database query performance

### MINOR (New features) - `1.X.0`
- Added a new feature
- Backward compatible (old code still works)
- Updated API with new endpoints

**Examples:**
- `1.0.0` → `1.1.0` - Added password reset feature
- `1.1.0` → `1.2.0` - Added user profile editing

### MAJOR (Breaking changes) - `X.0.0`
- Changed how something works
- Old code will break
- Users need to update their integration

**Examples:**
- `1.0.0` → `2.0.0` - Changed API response format
- `2.0.0` → `3.0.0` - Removed deprecated endpoints

## During Development

While in the sprint, you DON'T version yet. You just work on features in `dev`.

### Example Development Cycle

```
Sprint 1:
  - Create features on feature branches
  - Merge to dev as they're done
  - dev grows with multiple features

Sprint 1 End:
  - Create release branch: release/v1.0.0
  - Test everything together
  - Create PR to main
  - Merge to main
  - Tag: git tag -a v1.0.0 -m "First release"
  - Push tag: git push origin v1.0.0
  - dev continues with new work

Sprint 2:
  - Build new features (maybe v1.1.0 or v1.0.1 depending on content)
  - Repeat process
```

## How to Tag a Release

### Step 1: Make Sure You're on Main

```bash
git checkout main
git pull origin main
```

### Step 2: Create an Annotated Tag

```bash
git tag -a v1.0.0 -m "Release v1.0.0: User authentication system"
```

### Step 3: Push the Tag

```bash
git push origin v1.0.0
```

### Step 4: View All Tags

```bash
git tag -l              # List all tags
git show v1.0.0         # See details of specific tag
```

## CommitEd Versioning Rules

For CommitEd (our project):

**Current Status:** 
- Start with `0.1.0` (pre-release)
- Not yet `1.0.0` (first stable release)

**Version 0.x.y Pattern:**
- `0.0.1` → `0.0.2` - Bug fixes during development
- `0.1.0` - First feature set complete
- `0.2.0` - Second major feature set complete
- `1.0.0` - Production ready with all core features

**When We Hit 1.0.0:**
- All core microservices stable
- Full authentication & authorization working
- Complete API documentation
- Performance tested
- Ready for actual users

## Coordinating Versions Across Microservices

Since CommitEd uses microservices, each service can have its own version!

### Approach 1: Independent Versioning (Recommended for you)

Each microservice versions independently:

```
CommitEd main project:  v1.0.0
├─ auth-service:       v1.2.0
├─ user-service:       v1.0.1
├─ project-service:    v1.1.0
└─ notification-service: v1.0.0
```

**Pros:**
- Services evolve at their own pace
- Don't wait for one slow service
- Clearer what changed where

**Cons:**
- More complex tracking
- Need clear dependency documentation

**Your approach:** Each service has own `main` branch and tags

### Approach 2: Monorepo Versioning (Simpler)

One version for everything:

```
CommitEd v1.0.0
├─ auth-service:       (included)
├─ user-service:       (included)
├─ project-service:    (included)
└─ notification-service: (included)
```

**Pros:**
- Simple to understand
- Everything tested together
- One tag covers everything

**Cons:**
- Can't release one service without others
- Smaller bug fix forces version bump everywhere

## Version in Your Code

### package.json (Node.js)

```json
{
  "name": "committed-auth-service",
  "version": "1.0.0",
  "description": "Authentication microservice for CommitEd"
}
```

### pom.xml (Java/Maven)

```xml
<project>
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.committed</groupId>
  <artifactId>auth-service</artifactId>
  <version>1.0.0</version>
</project>
```

### Python setup.py

```python
setup(
    name='committed-auth-service',
    version='1.0.0',
    description='Authentication service for CommitEd'
)
```

### Docker Image Tags

```bash
docker tag committed-auth:latest committed-auth:1.0.0
docker push committed-auth:1.0.0
```

## Release Checklist

Before tagging a release:

- [ ] All features merged to dev
- [ ] All tests passing
- [ ] Documentation updated (README, API docs)
- [ ] CHANGELOG.md updated with what's new
- [ ] Code reviewed by team
- [ ] No debug code or console.logs
- [ ] Version bumped in code (package.json, etc.)
- [ ] Create release branch: `release/v1.0.0`
- [ ] PR to main, get approval
- [ ] Merge to main
- [ ] Tag the commit: `git tag -a v1.0.0 -m "..."`
- [ ] Push tag: `git push origin v1.0.0`

## CHANGELOG.md Example

Track what changed in each version:

```markdown
# Changelog

All notable changes to this project will be documented in this file.

## [1.0.0] - 2025-12-15

### Added
- User authentication with JWT tokens
- Email verification on signup
- Password reset functionality
- User profile management

### Fixed
- Session timeout bug
- Database connection pooling

### Changed
- API response format (breaking change!)
- Error message clarity

## [0.2.0] - 2025-12-01

### Added
- User registration endpoint
- Email templates

## [0.1.0] - 2025-11-15

### Added
- Initial project setup
- Basic API structure
```

## Communicating Versions

### Release Notes

When you tag a release, include a clear message:

```bash
git tag -a v1.0.0 -m "CommitEd v1.0.0: Authentication system

Added:
- User signup and login
- JWT token management
- Email verification
- Password reset

Breaking Changes:
- /api/v1/ endpoints now require 'Authorization' header

Fixed:
- Session timeout after 24 hours
- Database query optimization"
```

### GitHub Releases

On GitHub, go to Releases → Create Release:

```
Title: CommitEd v1.0.0 - Authentication System

Description:
## What's New
- ✨ User authentication
- ✨ Email verification
- 🐛 Fixed session timeout

## Breaking Changes
- API response format changed

## Contributors
@alice @bob @charlie

## Installation
See README.md for setup
```

## Version Comparison

| Version | What Changed | When to Use |
|---------|--------------|-------------|
| 0.1.0 → 0.1.1 | Bug fix | Critical bug needs immediate release |
| 0.1.0 → 0.2.0 | New feature | Feature complete and tested |
| 0.9.0 → 1.0.0 | Production ready | All core features, stable |
| 1.0.0 → 1.0.1 | Small fix | Patch for existing users |
| 1.0.0 → 1.1.0 | New feature | New feature, backward compatible |
| 1.9.0 → 2.0.0 | Breaking change | Major redesign or API change |

## During Sprints: Version Planning

### Sprint Planning

Discuss version number:

**"Should we bump to 1.0.0 this sprint or stay at 0.5.0?"**

Factors:
- Is everything stable?
- Are we production ready?
- Will this break existing users?
- Is this a significant milestone?

### Sprint Goal + Version

Example sprint goal:

```
Sprint Goal: Release v1.0.0 - Full Authentication System

Includes:
- User signup, login, logout
- Email verification
- Password reset
- JWT token refresh

Version: MAJOR bump (0.9.0 → 1.0.0)
Reason: Authentication is core foundation, now stable
```

## Quick Reference

**Increment PATCH** (X.Y.Z → X.Y.Z+1):
- Bug fixes only
- No new features
- No breaking changes

**Increment MINOR** (X.Y → X.Y+1.0):
- New features
- Backward compatible
- Old code still works

**Increment MAJOR** (X → X+1.0.0):
- Breaking changes
- API changes
- Removal of features

## Common Mistakes to Avoid

❌ **Don't:**
- Use timestamps as versions (v2025-11-30)
- Jump versions randomly (1.0.0 → 5.0.0)
- Forget to document what changed
- Tag commits without PR/review
- Use different format per service

✅ **Do:**
- Use semantic versioning consistently
- Document in CHANGELOG.md
- Tag only after merging to main
- Include clear release notes
- Keep all services' versioning clear
