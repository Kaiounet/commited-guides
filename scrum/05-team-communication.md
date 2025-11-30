# Team Communication & Coordination

## Communication Channels

### Synchronous (Real-time)

**Standups** (Daily, 10 min)
- What: Quick sync on progress
- When: Morning before work
- How: In-person or video call

**Code Review Comments** (On GitHub)
- What: Feedback on PRs
- Response time: Within 24 hours

**Slack/Discord** (As needed)
- What: Questions, blockers, quick decisions
- Use for: Urgent issues, quick clarifications

### Asynchronous (Delayed)

**GitHub Issues** (Tracked and documented)
- What: Bug reports, feature requests, discussions
- Response time: Within 48 hours

**PR Descriptions** (In code)
- What: Why the change was made
- Benefit: Future team members understand decisions

**Retrospective Notes** (End of sprint)
- What: Lessons learned and improvements
- Who reads: Whole team

## Conflict & Decision-Making

### When You Disagree

**Example**: "Should we use React or Vue?"

**Process**:
1. **Listen**: Understand the other perspective fully
2. **Discuss**: Share your reasoning
3. **Decide**: Tech lead makes final call if no consensus
4. **Commit**: Everyone supports the decision
5. **Document**: Record reasoning in a comment

**Never**:
- ❌ Go rogue and use your preferred tech anyway
- ❌ Argue endlessly in Slack
- ❌ Passive-aggressively ignore the decision

**Example GitHub comment**:
```
Discussed React vs Vue in standup:

React: Better for team (2 know it), more community support
Vue: Simpler to learn

Decision: Use React

Reasoning: Team velocity is critical in academic setting.
Going with what team knows best.

Next time: Establish tech choices earlier in project.
```

## When Someone's Not Pulling Their Weight

**Approach** (not confrontation):
1. **In standup**: "John, you said you'd have X done. Blocker?"
2. **If pattern emerges**: Talk privately
3. **Tech lead involvement**: If needed
4. **Support**: Maybe they need help, not criticism

**Never**:
- ❌ Complain in group chat
- ❌ Do their work without asking
- ❌ Create drama

## Remote Team Considerations

### Video Standups
- ✅ Cameras on (see each other)
- ✅ Short and focused
- ✅ Post summary in Slack after

### Timezone Challenges
- Plan sprints to minimize overlap needs
- Record decisions and post them immediately
- Async-first: Use GitHub for discussions

### Building Trust
- Consistent communication
- Follow through on commitments
- Assume good intent
- Celebrate wins publicly

## Documentation Standards

### What Gets Documented
- **Decisions**: Why we chose tech X over Y
- **Complex code**: How tricky algorithms work
- **Setup**: How new team members get running
- **API changes**: Breaking changes need notice
- **Bugs**: Lessons learned from incidents

### Where to Document
- **README.md**: Setup and overview
- **Code comments**: Complex logic only
- **PR descriptions**: What and why
- **Wiki or Docs folder**: Deep dives
- **GitHub Issues**: Decisions and discussions

### What NOT to Document
- ❌ Obvious code (if it's clear, don't comment)
- ❌ Project status (use Jira/GitHub Projects)
- ❌ Meeting notes (unless decisions made)

## Tools Setup for Communication

### Minimum (For Academic Projects)
```
GitHub
  ├─ Issues: Task tracking
  ├─ Projects: Board view
  ├─ PR comments: Code discussion
  └─ Discussions: Async conversation

Google Meet/Zoom: Standups

Slack: Quick questions
```

### Nice to Have
```
GitHub Wiki: Detailed documentation
Loom: Video explanations
Google Docs: Collaborative design docs
Figma: Shared design mockups
```

## Meeting Agenda Templates

### Sprint Planning
```
Duration: 1.5-2 hours

1. Product Owner vision (10 min)
2. Backlog refinement (20 min)
3. Team estimation (20 min)
4. Sprint goal definition (10 min)
5. Task breakdown (20 min)
6. Questions & close (10 min)
```

### Sprint Review
```
Duration: 1 hour

1. Sprint goal recap (5 min)
2. Demonstration of work (40 min)
3. Feedback & acceptance (10 min)
4. Celebration & announcements (5 min)
```

### Retrospective
```
Duration: 45 minutes

1. What went well? (10 min, sticky notes)
2. What didn't? (10 min, sticky notes)
3. Discussion & patterns (15 min)
4. Action items & owner (10 min)
```

## Onboarding New Team Members

### First Day Checklist
- [ ] Account access (GitHub, Slack, etc.)
- [ ] Repo cloned locally
- [ ] Development environment running
- [ ] Read README and architecture docs
- [ ] Meet the team in person/video

### First Week
- [ ] Assigned to simple task (documentation or small fix)
- [ ] Pair with experienced person on a feature
- [ ] Attend all standups
- [ ] Make first PR and get feedback
- [ ] Run project locally end-to-end

### First Sprint
- [ ] Carry own tasks
- [ ] Ask questions freely
- [ ] Contribute in retrospective
- [ ] Help someone else if ahead

## Team Rituals (Non-Required but Nice)

- **Celebrate merges**: "Nice work on that PR!" in Slack
- **Weekly wins**: Friday recap of what shipped
- **Learning share**: 15 min Tuesday where someone shares what they learned
- **Social chat**: #random for off-topic (builds culture)

## Red Flags

🚩 **If your team has these, talk to the tech lead:**
- Communication breakdowns
- People working in silos (never talking)
- Decisions made without group input
- PR reviews taking >48 hours
- Standups skipped regularly
- Conflicts brewing silently
- Someone seems overwhelmed but won't say
