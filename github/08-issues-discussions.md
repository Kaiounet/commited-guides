# GitHub Issues & Discussions: Team Collaboration

## Overview

GitHub provides two main ways to collaborate:

- **Issues** - Track bugs, features, and tasks (actionable work)
- **Discussions** - Have conversations, brainstorm, ask questions (exploration)

Think of it this way:
- **Issue** = "Do this work" (has a clear deliverable)
- **Discussion** = "Let's talk about this" (exploring ideas)

## GitHub Issues

Issues are your task management system.

### Creating an Issue

**When to create:**
- Found a bug
- Want a new feature
- Have a task that needs doing
- Need to track technical debt

**Step 1: Title (Required)**

Clear, specific title:

```
✅ [FEATURE] Add password reset via email
✅ [BUG] Login timeout after 30 minutes
✅ [TASK] Update API documentation
✅ [REFACTOR] Split AuthController into separate files

❌ "Fix bug"
❌ "New stuff"
❌ "TODO"
```

**Step 2: Description (Required)**

For bugs:
```markdown
## Description
User cannot reset password when email is not verified.

## Steps to Reproduce
1. Sign up without verifying email
2. Click "Forgot Password"
3. Check email (nothing arrives)

## Expected Behavior
Should send reset link regardless of verification status

## Actual Behavior
No email is sent, no error message shown

## Environment
- Browser: Chrome 120
- Device: MacBook Pro
```

For features:
```markdown
## Description
Users should be able to export their project data as PDF.

## User Story
As a project owner
I want to export my project as PDF
So that I can share it offline

## Acceptance Criteria
- [ ] User can click "Export as PDF" button
- [ ] PDF includes project title, description, and tasks
- [ ] PDF downloads without errors
- [ ] File is named: "ProjectName_Date.pdf"

## Technical Notes
Could use pdfkit library (already in dependencies)
```

For tasks:
```markdown
## Description
Refactor user authentication module.

## What to do
- [ ] Extract JWT logic into separate class
- [ ] Add unit tests for token generation
- [ ] Update error messages for clarity
- [ ] Add documentation to public methods

## Files involved
- src/auth/AuthService.ts
- src/auth/JWTManager.ts

## Why?
Current code is 500+ lines, hard to test. Breaking it up makes it maintainable.
```

**Step 3: Labels (Recommended)**

Click "Labels" to add:
- `bug` - Something broken
- `feature` - New functionality
- `task` - General work
- `documentation` - Docs only
- `help-wanted` - Need expertise
- `good-first-issue` - Good for new team members
- `high-priority` - Do this soon
- `blocked` - Waiting on something else
- `frontend` / `backend` / `database` - Component labels
- `auth-service` / `user-service` - Service labels (for your microservices!)

**Step 4: Assign (Recommended)**

Assign to: Yourself or teammate starting the work

**Step 5: Project (Recommended)**

Add to GitHub Project board (see below)

### Managing Issues During Sprint

**Issue Board (Kanban)**

Move issues through columns:

```
Backlog → Todo → In Progress → In Review → Done
```

Your workflow:

1. **Backlog**: Created but not started
2. **Todo**: Ready to work on, assigned
3. **In Progress**: You're actively working
4. **In Review**: PR created, waiting for review
5. **Done**: PR merged, work complete

**Assigning Issues**

When you pick up work:
- Click "Assign yourself"
- Move to "In Progress"
- Create feature branch for it

**Linking PR to Issue**

In your PR description:

```markdown
## Changes
Implements password reset functionality

## Related Issue
Closes #42
```

When merged, issue automatically closes.

**If Stuck**

```markdown
## Comment
I'm blocked on the database query. 
@alice can you review the schema I'm using?

Status: moved to "blocked" label
```

### Issue Lifecycle for CommitEd

**Creation Phase**
- Title + description
- Add relevant labels
- Add to project board

**Development Phase**
- Assigned to someone
- Branch created: `feature/auth-reset-password`
- PR linked in comment: "Closes #42"
- Moved to "In Review"

**Completion Phase**
- PR approved
- Merged to dev
- Issue auto-closes
- Moved to "Done"

**Release Phase**
- Included in next version tag
- Added to CHANGELOG.md
- Referenced in release notes

## GitHub Discussions

Discussions are for conversations, not action items.

### When to Use Discussions

**YES - Create a Discussion:**
- How should we handle user permissions?
- What's the best way to structure our error responses?
- Should we use Redis or in-memory caching?
- Can someone explain how the auth flow works?
- What tools should we use for monitoring?

**NO - Create an Issue:**
- Implement feature X (create issue instead)
- Fix bug Y (create issue instead)
- This needs code change (create issue instead)

### Creating a Discussion

**Step 1: Category**

Choose one:
- **General** - Questions, thoughts, anything
- **Announcements** - Team announcements
- **Ideas** - Suggestions and brainstorms
- **Q&A** - Questions about code/architecture
- **Architecture** - Design decisions

**Step 2: Title**

```
✅ How should we handle service-to-service authentication?
✅ Should we use JWT or OAuth for external APIs?
✅ What's the best pattern for database transactions in microservices?

❌ "Question"
❌ "Help"
```

**Step 3: Description & Discussion**

**Example - Architecture Decision:**

```
Title: Should each microservice have its own database?

Description:
We're designing CommitEd's data layer. Options:

A) Shared database (easier joins)
B) Each service has own database (better isolation)

Pros/Cons:
Database per service:
  ✓ Scales independently
  ✓ Different databases if needed
  ✗ Complex joins
  ✗ Harder transactions

Shared database:
  ✓ Simple queries
  ✓ Easier relationships
  ✗ Tight coupling
  ✗ All services must use same DB

What should we choose for CommitEd?
```

**Team responds:**
```
Alice: I vote for database per service. Microservices should be independent.

Bob: But then how do we handle transactions across services?

Alice: Good point. We'd need eventual consistency patterns like event sourcing.

Charlie: That adds complexity. Maybe shared database for now, refactor later?
```

### Discussion to Issue Conversion

If a discussion leads to actionable work:

```
Alice: Everyone agrees - let's document our API error codes.

[Thread below marks this as the decision point]
```

Then create an issue:

```
Title: [TASK] Document all API error codes
Description: 
As decided in discussion #15, we need comprehensive API error documentation.

Include:
- All error codes (400, 401, 404, etc.)
- Error messages
- How to handle each on frontend
- Examples in documentation
```

Link back in discussion: "Created issue #47 to track this"

## Best Practices

### For Issues

**Title Format**
```
[TYPE] What needs to be done

Types: FEATURE, BUG, TASK, DOCS, REFACTOR, HOTFIX
```

**Description Clarity**
- Be specific
- Include context
- Link related issues
- Add visual examples if UI-related

**Keep It Focused**
- One feature per issue
- If too big, split it
- Example: Don't do "Complete auth system" (split into signup, login, password reset)

**Use Labels**
- Makes filtering easier
- Helps team see what's urgent
- Service labels show which microservice

**Assignment**
- Assign only when someone starts
- Otherwise it's "up for grabs"
- Change if plans shift

### For Discussions

**Ask Clear Questions**
```
✅ "How should we handle JWT token refresh?"
❌ "JWT?"
```

**Provide Context**
- Why are you asking?
- What problem are you solving?
- What have you already tried?

**Encourage Responses**
- Tag people: @alice @bob
- Ask for specific opinions
- Don't wait passively

**Document Decisions**
- Pin the final decision comment
- Convert to issue if needed
- Link in related code comments

## CommitEd Specific Guidelines

### Labels for Microservices

Since CommitEd uses microservices, add service labels:

```
🏷️ Services:
- auth-service
- user-service
- project-service
- notification-service
- api-gateway

Example issue:
Title: [BUG] User service fails when email has plus sign
Labels: bug, high-priority, user-service
```

### Issue Naming for Services

Include service in title:

```
✅ [FEATURE] Auth: Add two-factor authentication
✅ [BUG] User Service: Profile image upload fails
✅ [TASK] API Gateway: Update rate limiting

This makes it clear which service is affected
```

### Cross-Service Issues

For work spanning multiple services:

```markdown
Title: [TASK] Implement service-to-service authentication

## Services Affected
- [ ] auth-service (provide JWT validation)
- [ ] user-service (consume auth tokens)
- [ ] project-service (consume auth tokens)
- [ ] api-gateway (verify tokens)

## Coordination
These must be done in order:
1. auth-service validation (dependency)
2. user-service integration
3. project-service integration
4. gateway middleware

## Dependencies
Do NOT start until auth-service is complete
```

### Discussion Topics for Microservices

Good discussion topics:

```
"How should services communicate - REST, gRPC, or message queue?"
"Should each service have its own database or shared?"
"How do we handle distributed transactions?"
"What's our service discovery strategy?"
"How should we do inter-service authentication?"
```

## Example CommitEd Sprint Board

```
BACKLOG (No one assigned):
├─ [FEATURE] Auth: OAuth integration
├─ [BUG] User: Avatar upload size limit
└─ [DOCS] API: Update endpoint documentation

TODO (Ready to start):
├─ [FEATURE] Auth: Two-factor authentication (assigned: @alice)
├─ [TASK] User: Refactor profile endpoint (assigned: @bob)
└─ [FEATURE] Project: Add project templates (assigned: @charlie)

IN PROGRESS (Currently working):
├─ [BUG] Project: Sharing permissions bug (assigned: @alice)
│  PR: #98 (awaiting review)
└─ [FEATURE] Notification: Email notifications (assigned: @bob)
   PR: pending

IN REVIEW (Waiting for approval):
└─ [TASK] API: Error code documentation (assigned: @charlie)
   PR: #101 (2 approvals needed)

DONE (Merged this sprint):
├─ ✅ [FEATURE] Auth: Basic login/signup
├─ ✅ [FEATURE] User: Profile editing
└─ ✅ [BUG] Database: Query timeout optimization
```

## Quick Reference

### Create Issue When:
- Found a bug
- New feature needed
- Task to complete
- Technical debt
- Documentation needed

### Create Discussion When:
- Deciding on approach
- Brainstorming ideas
- Asking for advice
- Explaining architecture
- Gathering opinions

### Close Issue When:
- PR merged
- Bug fixed
- Feature complete
- Task done

### Pin Discussion When:
- Important decision made
- Needed for reference
- New team member should read

## Tips for Success

✅ **Clear is better than detailed**
- People scan, don't read novels
- Use bullet points
- Add examples

✅ **Link everything**
- Link related issues
- Link to discussions
- Link in PRs

✅ **Keep it organized**
- Use labels consistently
- Assign issues
- Use project board

✅ **Respond quickly**
- Check assigned issues daily
- Respond to questions in 24 hours
- Help teammates get unstuck

❌ **Don't:**
- Leave issues unassigned indefinitely
- Create vague titles
- Forget to close merged issues
- Let discussions go unanswered
