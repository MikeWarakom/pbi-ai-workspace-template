---
name: progress-tracker
description: Use this skill whenever the user wants to update tasks, log what they completed, plan next steps, or write an end-of-session summary. Trigger when the user says "I finished", "I completed", "what should I do next", "update my progress", or at the end of any work session. Also trigger when the user asks for a project status summary.
---

# Progress Tracker

Read, update, and summarise project progress. Plan next steps.
Write session handoffs for continuity between sessions.

## Behavior When Invoked
1. Read `progress.md` — current state
2. Read `requirements.md` — full scope to understand % complete
3. Read `session-handoff.md` — what was in flight last session
4. Apply user's update (what they completed today)
5. Move items between status buckets
6. Suggest next 2-3 priorities from backlog
7. Output full updated `progress.md`
8. Output updated `session-handoff.md` block to prepend

## progress.md Format to Maintain
```markdown
# Project Progress

**Project**: [Name]
**Sprint**: [Name or Number]
**Version**: [X.X] | **Last Updated**: [YYYY-MM-DD]

---

## 🔴 Blocked
- [ ] [Task] — blocked by: [reason] — since: [date]

## 🟡 In Progress
- [ ] [Task] — started: [date] — linked: [REQ-XXX]

## 🟢 Done
- [x] [Task] — completed: [date] — linked: [REQ-XXX]

## 📋 Backlog
- [ ] [Task] — priority: High — linked: [REQ-XXX]
- [ ] [Task] — priority: Medium — depends on: [other task]

---

## Session Log
### [YYYY-MM-DD] — Session Summary
- ✅ Completed: [list]
- 🟡 Still in progress: [list]
- 🔴 Blockers: [list]
- 📋 Recommended next: [top 2-3]
```

Read `references/examples.md` for a full worked example.

## Self-Review Checklist
- [ ] Every blocked item has a reason and date
- [ ] Every in-progress item links to a REQ
- [ ] Session log appended (not replaced)
- [ ] Version bumped in header
- [ ] session-handoff.md block also produced
