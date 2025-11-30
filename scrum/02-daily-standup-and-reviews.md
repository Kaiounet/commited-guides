# Daily Standups, Reviews, and Retrospectives

Now that you understand Scrum (01-overview), let's look at how days and sprints actually work.

## Daily Standup

The daily standup is your team's pulse check - 10 minutes to stay synchronized.

### When
- **Every morning** at the same time (e.g., 9:00 AM)
- For CommitEd: Pick time when all can join

### Duration
- **10 minutes maximum**
- Set a timer, keep it strict

### Who Attends
- Entire development team
- Scrum Master (if you have one)
- Product Owner (optional)

### Format: 3 Questions

Each person answers these 3 questions briefly:

**1. What did I complete yesterday?**
```
✅ "Implemented login endpoint and wrote tests"
✅ "Reviewed 2 PRs and fixed auth bug"
❌ "I worked on stuff"  (too vague!)
```

**2. What will I do today?**
```
✅ "Working on password reset feature"
✅ "Testing user profile page, then code review"
❌ "Continue on my task"  (which task?)
```

**3. Am I blocked? (Do I need help?)**
```
✅ "Yes - waiting for database schema from database team"
✅ "No, moving forward"
✅ "Blocked on #42 PR approval"
❌ "Not sure"  (if uncertain, say "let's discuss after")
```

### Example Standup

**Team of 3 people, 9:00 AM:**

**Alice:**
"Yesterday: Completed JWT token generation and tests. Today: Working on logout endpoint. Not blocked."

**Bob:**
"Yesterday: Set up Docker environment and reviewed Alice's code. Today: Writing integration tests. Blocked: waiting for database password from IT."

**Charlie:**
"Yesterday: Finished user profile UI. Today: Implementing profile update API. Not blocked."

**Tech Lead:**
"Great! Bob - I have the DB password, sending now. Keep going!"

**Total: 3 minutes**

### Standup Anti-Patterns

❌ **"I was busy"** (too vague)
✅ **"I fixed 3 bugs in the auth service"**

❌ **Long explanations** (that's what Slack is for)
✅ **One sentence per question**

❌ **Problem-solving mode** ("Wait, why didn't you...?")
✅ **Note blockers, discuss offline**

❌ **Silent team members** (participation is required)
✅ **Everyone speaks, even if just "not blocked"**

### Blocker Examples

| Blocker | What to Do |
|---------|-----------|
| "Waiting for API docs" | Tech lead creates docs or assigns someone |
| "Code review takes too long" | Speed up reviews (set SLA: 24 hours) |
| "Database schema missing" | Pair with database person to design it |
| "CI/CD broken" | Dev ops helps fix, not your problem to solve alone |
| "I don't understand the requirement" | Clarify with Product Owner now |

**Key: Don't silently struggle!**

## Sprint Tracking Board

During the sprint, move work through these stages:

```
Backlog → Todo → In Progress → In Review → Done
  ↓
Stories not yet started
```

### Using GitHub Projects for CommitEd

**Backlog Column:** Stories planned but not started
- All stories for this sprint live here initially
- Prioritized (important first)

**Todo Column:** Ready to work on
- No dependencies
- Clear acceptance criteria
- Estimated

**In Progress Column:** You're actively working
- Usually one per person
- Updated daily in standup
- Add notes about progress

**In Review Column:** PR created, waiting for approval
- PR linked in issue
- Someone reviewing code
- Update: "Waiting for @alice's review"

**Done Column:** Completed and merged
- PR merged to dev
- Tests passing
- Accepted by Product Owner

### Example Board State (Mid-Sprint)

```
BACKLOG (4 stories)        | TODO (3 stories)        | IN PROGRESS (2)   | IN REVIEW (1)      | DONE (5)
- Add caching layer        | - Create JWT tokens     | - Auth API        | - Password reset   | - User DB schema
- Email notifications      | - Password hashing      | - Unit tests      | PR #89             | - Login endpoint
- Notification dashboard   | - Logout endpoint       |                   | (waiting on Bob)   | - Session tests
- User preferences UI      |                         |                   |                    | - Email templates
                           |                         |                   |                    | - Error handling
```

## Sprint Review

At the end of the sprint, show what you built. Not just "done", but **working**.

### When
- **End of sprint** (e.g., Friday afternoon)
- Before retrospective
- Same day

### Duration
- **1 hour** for typical team

### Who Attends
- Entire team
- Product Owner / Instructor
- Interested stakeholders
- Clients (if external project)

### What Happens

**Step 1: Demo completed work**
- Run the software
- Show features working
- "Here's what we built"

**Step 2: Demonstrate acceptance criteria**
- "As a user, I can log in... [show it working]"
- "Password must be 8+ chars... [show validation]"
- Answer questions

**Step 3: Product Owner accepts or rejects**
- ✅ "Accepted! Great work!"
- 🔄 "Needs adjustment... move to next sprint"
- ✅ Usually most stuff is accepted

**Step 4: Celebrate**
- "We completed X stories!"
- "Great sprint!"
- Recognize effort

### Sprint Review Anti-Patterns

❌ **Showing code** (no one cares, show working software)
✅ **Demo in browser, running on server**

❌ **"Almost works, just need to..."** (not done!)
✅ **Only show completed, accepted work**

❌ **Making excuses** ("We tried our best...")
✅ **Explaining what you learned and built**

❌ **Rushing through** (show your work with pride!)
✅ **Take time, answer questions, celebrate**

## Sprint Retrospective

After the review, the team reflects on **how you worked**, not what you built.

### When
- **Same day as review** (Friday afternoon)
- After 15-30 min break
- Separate from review

### Duration
- **30-45 minutes**

### Who Attends
- **Just the development team**
- NOT Product Owner usually
- NOT external people

**Why private?** Safe space to be honest about problems

### Format: "What. So What. Now What."

**1. What went well?** (5 min)
```
- Standup kept us coordinated
- PR reviews were quick and helpful
- Good documentation made onboarding easy
- We finished everything we planned!
```

**2. What didn't go well?** (5 min)
```
- Too many meetings
- Git conflicts slowed us down
- Estimation was off
- One person blocked for 2 days
```

**3. What will we improve next sprint?** (5 min)
```
- Limit meetings to 30 min max
- Have weekly git workshop
- Better story point estimation
- Pair programming when blocked
```

**4. Action items** (10 min)
```
- Pair programming protocol (John to write guide)
- Estimation workshop (Tech lead to facilitate)
- Git conflict prevention (Team lead)
- Only 2 meetings per week (Everyone agrees)
```

### Retrospective Tips

**Be honest:**
- It's safe to admit mistakes
- Problems help you improve
- Don't hide issues

**Focus on process, not people:**
- ✅ "PRs take too long" (process issue)
- ❌ "Bob is slow at code review" (person blame)

**Make it actionable:**
- ✅ "Limit meetings to 30 min" (specific action)
- ❌ "Communicate better" (vague)

**Assign owners:**
- ✅ "John will document pair programming"
- ❌ "Someone should write a guide"

## Velocity & Planning

### What is Velocity?

How many story points your team completes per sprint.

```
Sprint 1: 22 points ✓ (4 features done, 1 blocked)
Sprint 2: 25 points ✓ (good estimation this time)
Sprint 3: 20 points ✓ (one person sick, that's ok)
Sprint 4: 24 points ✓ (very consistent now)
Sprint 5: 26 points ✓ (getting better!)

Average: ~23 points per sprint
```

### Why Track Velocity?

**Predictable planning:**
- "We do ~23 points per sprint"
- "Project is 200 points"
- "That's ~8-9 sprints to finish"

**Realistic commitments:**
- Don't commit to 40 points if you average 23
- Better to underestimate and deliver
- Builds team credibility

**Identify problems:**
- Velocity drops → blockers/issues
- Velocity increases → team improving
- Stable → predictable

### Using Velocity for CommitEd

After Sprint 1:
- Document actual story points completed
- Use that for Sprint 2 planning
- Adjust estimates based on learning

By Sprint 3-4:
- Should have reliable velocity
- Can plan end-of-project timeline
- Can predict when features ship

## Common Sprint Issues & Solutions

### "We overcommitted"
```
What happened: Committed to 35 points, completed 20

Why: Bad estimation, unexpected blockers, scope creep

Solution:
  1. Drop lowest-priority items to backlog
  2. Finish what you can
  3. In retrospective: Estimate more conservatively
  4. Next time: Build in buffer (don't use 100% capacity)
```

### "Someone's stuck"
```
Signal: Standup - "I'm blocked on X"

Immediate action:
  1. Team helps unblock (not alone for 2+ hours)
  2. Pair programming if needed
  3. Escalate if needed (tech lead)
  4. Document lesson learned

Next sprint:
  1. Retro discusses prevention
  2. Add process improvement
```

### "Scope keeps growing"
```
Mid-sprint: "Wait, we also need feature Y"

Solution:
  1. "That's a new story for the backlog"
  2. Don't add to current sprint
  3. Plan for next sprint
  4. Keep focus on sprint goal

Why: Changing mid-sprint breaks planning and stress

Key: "Scope grows, but we finish what we start"
```

### "Velocity fluctuates wildly"
```
Velocities: 20, 35, 18, 40, 22

Signs: Estimation is off or too many unknown factors

Improvement:
  1. Estimation workshop (learn points together)
  2. Break down big stories more
  3. Track blockers (external delays)
  4. Better story definition
  5. See "Velocity" section - this stabilizes over time
```

## Tips for Successful Standups & Sprints

✅ **Be on time** - Shows respect for team

✅ **Be specific** - Not "working on features" but "debugging login API"

✅ **Be realistic** - Estimate based on complexity, not hope

✅ **Communicate blockers early** - Don't wait 2 days

✅ **Help each other** - Standup signals who needs support

✅ **Update the board** - Keep it accurate for others

✅ **Celebrate progress** - Sprint review is important for morale

✅ **Learn & improve** - Retro should change how you work next sprint

## Quick Reference

### Daily Standup
- 10 min, every morning
- 3 questions each person
- Signal blockers

### Sprint Tracking
- Kanban board (Backlog → Done)
- GitHub Projects for CommitEd
- Updated daily

### Sprint Review
- 1 hour, end of sprint
- Demo working software
- Product Owner accepts

### Sprint Retrospective
- 30-45 min, end of sprint
- Team only (no Product Owner)
- What went well? What didn't? What to change?
