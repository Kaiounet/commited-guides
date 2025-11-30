# Microservices Development Workflow

## CommitEd Architecture

CommitEd uses **microservices**: Instead of one big application, you have multiple small, independent services that work together.

### CommitEd Services (Example)

```
api-gateway/
├─ Routes requests to services
├─ Handles authentication
└─ Rate limiting & logging

auth-service/
├─ User login/signup
├─ Token generation
└─ Permission checks

user-service/
├─ User profiles
├─ User preferences
└─ Account settings

project-service/
├─ Project CRUD
├─ Project permissions
└─ Project sharing

notification-service/
├─ Email notifications
├─ In-app notifications
└─ Notification preferences
```

## Why This Matters for Your Workflow

In a monolith (one big app), everything shares the same codebase. In microservices:

- ✅ Services are independent
- ✅ Each can deploy separately
- ✅ Different teams can work on different services
- ✅ Easier to scale individual services

But it means:

- ⚠️ More coordination needed
- ⚠️ Services must communicate somehow
- ⚠️ Naming/versioning matters across services
- ⚠️ Dependency management is complex

## Repository Structure

### Option 1: Monorepo (Recommended for CommitEd)

One repository with all services:

```
committed/
├─ README.md (overall project guide)
├─ docker-compose.yml (local development)
├─ .github/
│  └─ workflows/ (shared CI/CD)
│
├─ api-gateway/
│  ├─ src/
│  ├─ tests/
│  ├─ Dockerfile
│  ├─ package.json
│  └─ README.md (service-specific)
│
├─ auth-service/
│  ├─ src/
│  ├─ tests/
│  ├─ Dockerfile
│  ├─ package.json
│  └─ README.md
│
├─ user-service/
│  ├─ src/
│  ├─ tests/
│  ├─ Dockerfile
│  ├─ package.json
│  └─ README.md
│
├─ project-service/
│  ├─ src/
│  ├─ tests/
│  ├─ Dockerfile
│  ├─ package.json
│  └─ README.md
│
└─ notification-service/
   ├─ src/
   ├─ tests/
   ├─ Dockerfile
   ├─ package.json
   └─ README.md
```

**Pros:**
- Easy to see all code together
- Shared dependencies simpler
- One git history
- Good for learning/small teams

**Cons:**
- Can be large
- All services must be checked out

### Option 2: Separate Repositories

Each service is its own repo:

```
committed-auth-service/
committed-user-service/
committed-project-service/
committed-notification-service/
committed-api-gateway/
```

**Pros:**
- Smaller repos
- Independent deployments
- Easier scaling

**Cons:**
- Need to clone multiple repos
- Version coordination harder
- More complex CI/CD

**For CommitEd (recommendation):** Use monorepo initially, convert to separate repos if team grows.

## Branch Naming for Microservices

### Standard Branch Naming

Include the service name:

```
feature/auth/two-factor-authentication
feature/user/profile-image-upload
feature/project/sharing-permissions
fix/notification/email-delivery-bug
docs/api-gateway/rate-limiting
refactor/user/database-queries
```

**Format:** `<type>/<service>/<description>`

### Why This Matters

```
✅ feature/auth/jwt-refresh       → Clear which service
✅ feature/user/settings-page     → Easy to find related PRs
❌ feature/new-auth-stuff         → Which service? What specifically?
❌ user-updates                   → Too vague, doesn't indicate service
```

### Service Abbreviations

For consistency, define short names:

```
api       - API Gateway
auth      - Auth Service
user      - User Service
project   - Project Service
notif     - Notification Service
```

So branches might be:

```
feature/api/rate-limiting
feature/auth/oauth
feature/user/avatar-upload
feature/project/templates
feature/notif/email-queue
```

## Commit Messages for Microservices

Include the service in your commits:

```bash
git commit -m "feat(auth): add JWT token refresh endpoint"
git commit -m "fix(user-service): profile image upload validation"
git commit -m "docs(api-gateway): update rate limit documentation"
```

**Scope format:** `(service-name)`

## Pull Requests in Microservices

### Single-Service PR (Most Common)

Only changes one service:

```markdown
## Title
feat(auth): implement two-factor authentication

## Description
Users can now enable 2FA on their account.

## Services Changed
- auth-service (only)

## Testing
- [ ] Login with 2FA enabled
- [ ] Login with 2FA disabled
- [ ] 2FA setup flow
- [ ] Recovery codes work

## Deployment
This is backwards compatible. Can merge anytime.
```

### Cross-Service PR (Requires Coordination)

Changes affect multiple services:

```markdown
## Title
feat: add JWT token refresh flow

## Services Changed
- auth-service (provides refresh endpoint)
- user-service (calls refresh endpoint)
- api-gateway (includes refresh in middleware)

## Order of Deployment
1. auth-service first (new endpoint)
2. api-gateway next (middleware update)
3. user-service last (uses refresh)

## Important
DO NOT merge all at once. Must coordinate deployment.
Alice: Merge auth-service first
Bob: Then I'll merge api-gateway
Charlie: Finally user-service
```

### Dependencies Between Services

Always document if one service depends on another:

```markdown
## Dependencies
This PR depends on auth-service #95 being deployed first.
PR #95 adds the new JWT validation endpoint.

Do not merge this until auth-service is live!
```

## Development: Running Everything Locally

### With Docker Compose

Create `docker-compose.yml` in root:

```yaml
version: '3.8'

services:
  postgres:
    image: postgres:15
    environment:
      POSTGRES_PASSWORD: password
    ports:
      - "5432:5432"

  auth-service:
    build: ./auth-service
    ports:
      - "3001:3000"
    environment:
      DATABASE_URL: postgres://postgres:password@postgres:5432/auth
    depends_on:
      - postgres

  user-service:
    build: ./user-service
    ports:
      - "3002:3000"
    environment:
      DATABASE_URL: postgres://postgres:password@postgres:5432/users
      AUTH_SERVICE_URL: http://auth-service:3000
    depends_on:
      - postgres
      - auth-service

  project-service:
    build: ./project-service
    ports:
      - "3003:3000"
    environment:
      DATABASE_URL: postgres://postgres:password@postgres:5432/projects
      AUTH_SERVICE_URL: http://auth-service:3000
    depends_on:
      - postgres
      - auth-service

  api-gateway:
    build: ./api-gateway
    ports:
      - "3000:3000"
    environment:
      AUTH_SERVICE_URL: http://auth-service:3001
      USER_SERVICE_URL: http://user-service:3002
      PROJECT_SERVICE_URL: http://project-service:3003
    depends_on:
      - auth-service
      - user-service
      - project-service
```

**Start everything:**
```bash
docker-compose up
```

**Stop everything:**
```bash
docker-compose down
```

### Local Development

For faster development, run services individually:

```bash
# Terminal 1: Auth service
cd auth-service
npm install
npm run dev          # Runs on :3001

# Terminal 2: User service
cd user-service
npm install
npm run dev          # Runs on :3002

# Terminal 3: API Gateway
cd api-gateway
npm install
npm run dev          # Runs on :3000
```

Environment variables in `.env`:

```
# auth-service/.env
PORT=3001
DATABASE_URL=postgres://localhost/auth

# user-service/.env
PORT=3002
DATABASE_URL=postgres://localhost/users
AUTH_SERVICE_URL=http://localhost:3001

# api-gateway/.env
PORT=3000
AUTH_SERVICE_URL=http://localhost:3001
USER_SERVICE_URL=http://localhost:3002
PROJECT_SERVICE_URL=http://localhost:3003
```

## Versioning Each Service

Each microservice can have its own version!

### package.json per Service

```
auth-service/package.json:
{
  "name": "committed-auth-service",
  "version": "1.2.0"
}

user-service/package.json:
{
  "name": "committed-user-service",
  "version": "1.0.1"
}

project-service/package.json:
{
  "name": "committed-project-service",
  "version": "1.1.0"
}
```

### Docker Image Versioning

```bash
# Build each service with its version
docker build -t committed-auth:1.2.0 ./auth-service
docker build -t committed-user:1.0.1 ./user-service
docker build -t committed-project:1.1.0 ./project-service

# Push to registry
docker push committed-auth:1.2.0
docker push committed-user:1.0.1
docker push committed-project:1.1.0
```

### Release Notes Per Service

When you release, document each service:

```markdown
# CommitEd v1.2.0 - December 2025

## auth-service v1.2.0 (NEW)
- Added JWT refresh token endpoint
- Fixed token expiration bug
- Breaking: Removed deprecated /login endpoint

## user-service v1.0.1 (PATCH)
- Fixed profile image upload validation

## project-service v1.1.0 (NEW)
- Added project templates
- Improved permission caching

## notification-service v1.0.0 (UNCHANGED)
- No changes this release
```

## Communication Between Services

### REST Endpoints

Services call each other:

```typescript
// In user-service, calling auth-service
async function validateToken(token: string) {
  const response = await fetch('http://auth-service:3000/validate', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ token })
  })
  return response.json()
}
```

### Message Queue (Optional, for async)

For better reliability, use message queue:

```typescript
// In user-service
await messageQueue.publish('user.created', {
  userId: newUser.id,
  email: newUser.email
})

// notification-service listens
messageQueue.subscribe('user.created', async (event) => {
  await sendWelcomeEmail(event.email)
})
```

### Service Discovery

As you grow, use service discovery:

```
In production:
  Instead of hardcoding: http://user-service:3000
  Use: http://committed-user-service.internal:3000
  (Or use service mesh like Istio/Linkerd)
```

## Testing Across Services

### Unit Tests (Per Service)

Each service tests itself:

```bash
cd auth-service
npm test         # Only auth-service tests
```

### Integration Tests (Multiple Services)

Test services working together:

```bash
# Start all services with docker-compose
docker-compose up

# Run integration tests
npm run test:integration
```

### Example Integration Test

```typescript
// tests/integration/user-signup.test.ts
describe('User Signup Flow', () => {
  test('Should create user and send verification email', async () => {
    // 1. Call user-service signup
    const signupRes = await fetch('http://localhost:3000/api/users/signup', {
      method: 'POST',
      body: JSON.stringify({ email: 'test@example.com', password: 'pass123' })
    })
    const user = await signupRes.json()

    // 2. Check auth-service created token
    const validateRes = await fetch('http://localhost:3001/validate', {
      method: 'POST',
      body: JSON.stringify({ token: user.token })
    })
    expect(validateRes.status).toBe(200)

    // 3. Check notification-service queued email
    const emails = await messageQueue.consumeMessages('email.send')
    expect(emails).toContainEqual(
      expect.objectContaining({ to: 'test@example.com' })
    )
  })
})
```

## Deployment for Microservices

### Local Development

```bash
docker-compose up          # All services at once
```

### Staging/Production

Deploy services independently:

```bash
# Deploy auth-service first (others depend on it)
docker tag committed-auth:1.2.0 registry.example.com/committed-auth:1.2.0
docker push registry.example.com/committed-auth:1.2.0
kubectl apply -f deploy/auth-service.yaml

# Wait for auth-service to be healthy
sleep 30

# Deploy other services
docker push registry.example.com/committed-user:1.0.1
kubectl apply -f deploy/user-service.yaml

docker push registry.example.com/committed-project:1.1.0
kubectl apply -f deploy/project-service.yaml

docker push registry.example.com/committed-api:2.0.0
kubectl apply -f deploy/api-gateway.yaml
```

## Best Practices for CommitEd Microservices

✅ **Do:**
- Include service name in branch names
- Include service name in commits
- Document service dependencies
- Have `.env.example` in each service
- Test locally with docker-compose before PR
- Document cross-service changes in PR description
- Version each service independently
- Deploy services in dependency order

❌ **Don't:**
- Change multiple services without coordination
- Forget to update documentation
- Leave services in broken state
- Merge cross-service PRs without checking dependencies
- Hardcode service URLs (use environment variables)
- Deploy services in random order

## Quick Reference

### Service Names (For Branches/Commits)

| Service | Branch Prefix | Commit Scope |
|---------|---------------|--------------|
| API Gateway | `feature/api/...` | `(api)` |
| Auth | `feature/auth/...` | `(auth)` |
| User | `feature/user/...` | `(user)` |
| Project | `feature/project/...` | `(project)` |
| Notification | `feature/notif/...` | `(notif)` |

### Starting Development

```bash
# Clone repo
git clone <committed-repo>

# Start all services
docker-compose up

# Services available at:
# API Gateway:       http://localhost:3000
# Auth Service:      http://localhost:3001
# User Service:      http://localhost:3002
# Project Service:   http://localhost:3003
# Notification Svc:  http://localhost:3004
```

### Making a Change to One Service

```bash
# 1. Create service-specific branch
git checkout -b feature/user/profile-image

# 2. Make changes in user-service/
# cd user-service && make changes

# 3. Test locally
docker-compose up
# Visit http://localhost:3002 to test

# 4. Commit with service scope
git commit -m "feat(user): add profile image upload"

# 5. Push and create PR
git push origin feature/user/profile-image
# Create PR in GitHub
```
