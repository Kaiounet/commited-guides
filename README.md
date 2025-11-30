# CommitEd - Your Development Team's Professional Guide

A comprehensive guide system written by a **software architect** for your **student development team**. Everything here is designed to be used **daily as you build your project professionally**.

## You Should Know This

We're not just learning tools—we're learning **how professional software teams work**. This framework teaches real practices you'll use at any company.

## Start Here

**New to the project?** Read these in order (2-3 hours):

1. **git/01-basics.md** (15 min) - Get Git working
2. **github/01-collaboration-basics.md** (20 min) - Your first PR
3. **github/05-project-standards.md** (20 min) - How we work together
4. **scrum/04-sprint-mechanics.md** (20 min) - How sprints work
5. **Bookmark github/06-quick-reference.md** - Your daily cheat sheet

Then **make your first commit and PR** to solidify it.

## The Big Picture

### Branch Strategy

Think of our branches like stages in production:

```
main          Production releases (stable, working code)
  ↑ PR when feature is done
dev           Development staging (where team code merges)
  ↑ PRs from feature work
feature/*     Your individual work (isolated, experimental)
```

**Why this matters:**
- `main` is always deployable (no broken code)
- `dev` is where the team works together
- Your branch is safe to experiment
- Everything goes through code review

### Sprint Rhythm

**1 week = 1 sprint**

- **Monday morning**: Plan what you'll build (story points, assignments)
- **Tue-Thu**: Build it (daily 10-min standups keep team synced)
- **Friday**: Demo what you built, then discuss improvements

Repeat. Every week you get better.

## How We Work

### Your Daily Workflow

**Morning:**
```bash
git checkout dev
git pull origin dev              # Get latest team changes
git checkout feature/your-task
git rebase origin/dev            # Sync with team
```

**During work:**
```bash
# Regular commits (not one giant commit at end)
git status
git add .
git commit -m "type(scope): what you did"
git push origin feature/your-task
```

**Before lunch/end of day:**
```bash
git log --oneline -5            # Verify your commits look good
```

**Create PR on GitHub** when feature is complete.

### Code Review

Your teammates review your code before it merges. This is **good**, not punishment:

- ✅ Catches bugs
- ✅ Shares knowledge
- ✅ Maintains quality
- ✅ Everyone learns

**You review others' code too.** Be constructive, not harsh.

## Guide Categories

### 🔧 Version Control (Git)

- **01-basics.md** - Commands and workflow
- **02-commit-standards.md** - How to write good commits
- **03-branching.md** - Branch strategy explained
- **04-common-mistakes.md** - When things go wrong (and how to fix them)
- **05-team-workflow.md** - Patterns we use daily

**When to read:** Day 1, then as reference

### 🐙 Collaboration (GitHub)

- **01-collaboration-basics.md** - Your first day
- **02-pull-requests.md** - PR workflow and review
- **03-forking.md** - Contributing to open source (bonus)
- **04-academic-workflow.md** - Issues and planning
- **05-project-standards.md** - Code quality and structure
- **06-quick-reference.md** - Daily cheat sheet (bookmark this!)

**When to read:** Day 1-2, then bookmark quick-reference

### 🏃 Project Management (Scrum)

- **01-sprints.md** - Sprint concepts
- **02-user-stories.md** - How we describe work
- **03-backlog.md** - Managing our work pipeline
- **04-sprint-mechanics.md** - Standups, reviews, retros (the rhythm)
- **05-team-coordination.md** - How we communicate

**When to read:** Day 2-3, then ongoing

### 📖 Documentation (Typst)

- **01-basics.md** through **06-structure.md** - Typst syntax
- **07-technical-docs.typ** - Writing architecture and API docs

**When to read:** When you need to document something

## Core Principles

### 1. Code Review is Your Friend

- Someone reads your code before it ships
- They're not judging you, they're improving quality
- You do the same for others
- Everyone gets better

### 2. Small, Regular Commits

- 5 commits a day is better than 1 commit a day
- Easier to review
- Easier to find bugs
- Easier to understand history
- More backup (if local drive dies)

### 3. Clear Communication

- Commit message explains **why**, not just **what**
- PR description explains the problem you solved
- Standup tells team what you're working on
- Ask for help before stuck 2+ hours

### 4. Quality First

- Tests before merging
- Documentation with code
- Code review before production
- "Done" means working AND reviewed AND tested

### 5. Professional Practices

- You're learning how real teams work
- These practices scale to 100+ person companies
- Your first job will use something similar
- Build good habits now

## Your Responsibilities

### Every Day
- ✅ Make a commit or two (small, focused)
- ✅ Push to have backup
- ✅ Attend standup
- ✅ Review a PR from teammate

### Every Sprint
- ✅ Estimate your tasks realistically
- ✅ Merge features to dev
- ✅ Participate in review and retro
- ✅ Help teammates when blocked

### Quality Standards
- ✅ Write tests for your code
- ✅ Follow code standards
- ✅ Document complex logic
- ✅ No debug code in PRs

## Team Standards

### Definition of "Done"

A feature is done when:
- [ ] Code written
- [ ] Tests passing
- [ ] PR reviewed and approved
- [ ] Merged to dev
- [ ] Documentation updated
- [ ] No regressions in other features

### Code Review Expectations

Response time: **Within 24 hours**

Good reviewers:
- Read the description first
- Understand what problem is being solved
- Check if tests exist
- Look for obvious bugs
- Give constructive feedback
- Approve or request changes

### Story Points (Estimation)

How much effort does a task take?

- **1 point** = 30 minutes (trivial)
- **3 points** = 1-2 hours (small)
- **5 points** = half day (medium)
- **8 points** = 1-2 days (large)
- **13 points** = 3+ days (very large, should split)

Be realistic. Better to underestimate and deliver than overestimate and delay.

## Getting Help

If you're stuck:

**Step 1:** Check the relevant guide (probably in this folder)
**Step 2:** Search existing code for similar solution
**Step 3:** Ask on Slack/Discord with context
**Step 4:** Pair with teammate if stuck >30 min
**Step 5:** Tell standup you're blocked

**Never:** Silently struggle or hack around the problem.

## Success Looks Like

### After First Week
- ✅ First PR merged
- ✅ Git workflow comfortable
- ✅ Understand branch strategy
- ✅ Can read/write commits

### After First Month
- ✅ Multiple PRs merged
- ✅ Review others' code confidently
- ✅ Comfortable with Git
- ✅ Story estimation reasonable

### By End of Project
- ✅ 100+ commits (evenly distributed)
- ✅ Complex features integrated
- ✅ Tests provide confidence
- ✅ Professional documentation
- ✅ Can explain architecture
- ✅ Ready for real development job

## The Tools

- **Git** - Version control
- **GitHub** - Collaboration
- **Scrum** - Project management
- **Typst** - Professional documentation
- **IDE/Terminal** - Your editor

All documented here with examples you'll actually use.

## Reading by Experience Level

### I'm New (First sprint)
- git/01-basics.md ✓
- github/01-collaboration-basics.md ✓
- github/05-project-standards.md ✓
- scrum/04-sprint-mechanics.md ✓
- github/06-quick-reference.md (bookmark!)

### I'm Getting Comfortable (Sprint 2-3)
- git/02-commit-standards.md (improve quality)
- github/04-academic-workflow.md (manage issues)
- scrum/05-team-coordination.md (communication)
- git/04-common-mistakes.md (reference when stuck)

### I'm Proficient (Sprint 4+)
- Reference as needed
- Help teammates learn
- Suggest improvements
- Mentor new people

## Quick Reference

### Commands You Use Daily

```bash
# Start your day
git checkout dev && git pull origin dev

# Work on your task
git checkout -b feature/task-name
git status                    # What changed?
git add .                     # Stage changes
git commit -m "type: message" # Save it
git push origin feature/task-name

# When done
# Create PR on GitHub, get review, merge

# After merge
git checkout dev && git pull origin dev  # Back to main
```

### Commit Message Format

```
feat(scope): what you added
fix(scope): what you fixed  
docs(scope): documentation change
refactor(scope): code improvement
test(scope): test addition
```

Example: `feat(auth): add JWT token validation`

### PR Checklist (Before Submitting)

- [ ] Tests pass locally
- [ ] No console.logs or debug code
- [ ] PR description explains what and why
- [ ] Linked to related issue
- [ ] Code follows project style
- [ ] Ready for teammate to review

## Need Something Specific?

| Problem | Solution |
|---------|----------|
| "How do I start?" | Read this README then git/01-basics.md |
| "Git is broken" | Check git/04-common-mistakes.md |
| "How do I review code?" | See github/02-pull-requests.md |
| "What's the workflow?" | Read github/05-project-standards.md |
| "I need commands" | See github/06-quick-reference.md |
| "Standup happening now?" | See scrum/04-sprint-mechanics.md |
| "How do I write docs?" | See typst/07-technical-docs.typ |
| "I'm blocked" | Slack team or ask in standup |

## This Isn't Busy Work

Everything here serves a purpose:

- ✅ **Git/GitHub** - Collaboration and code quality
- ✅ **Scrum** - Team organization and communication
- ✅ **Typst** - Professional documentation
- ✅ **Standards** - Sustainable, maintainable code

Professional teams use versions of all of this. You're learning real skills.

---

**Start with:** git/01-basics.md

**Bookmark:** github/06-quick-reference.md

**Questions?** Check the guide index above.
