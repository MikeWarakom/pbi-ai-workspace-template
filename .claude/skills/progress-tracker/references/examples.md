# Progress Tracker Examples

## Example — End of Session Update

**User says**: "I finished the Total Sales measure and Sales YTD. Still working on the regional breakdown. Blocked on prior year — waiting for client to confirm fiscal year definition."

**Updated progress.md buckets**:

Moves to 🟢 Done:
- [x] Total Sales measure — completed: 2024-02-20 — linked: REQ-001
- [x] Sales YTD measure — completed: 2024-02-20 — linked: REQ-002

Keeps in 🟡 In Progress:
- [ ] Regional breakdown visual — started: 2024-02-20 — linked: REQ-004

Moves to 🔴 Blocked:
- [ ] Prior Year comparison — blocked by: fiscal year definition pending client — since: 2024-02-20 — linked: REQ-005

**Session log entry to append**:
```markdown
### 2024-02-20 — Session Summary
- ✅ Completed: Total Sales measure, Sales YTD measure
- 🟡 Still in progress: Regional breakdown visual
- 🔴 Blockers: Prior year — awaiting fiscal year clarification from client
- 📋 Recommended next: Regional breakdown visual (REQ-004), Sales by Category (REQ-006)
```

---

## Example — session-handoff.md block to prepend

```markdown
## Session: 2024-02-20
**Focus**: DAX measures — base and time intelligence

### Completed
- Total Sales measure (REQ-001)
- Sales YTD measure (REQ-002)

### In Progress
- Regional breakdown visual (REQ-004) — started, not finished

### Blockers
- Prior Year comparison (REQ-005) — waiting on client to confirm fiscal year: calendar vs April start

### Decisions Made
- Using DATESYTD for YTD — logged in decisions.md (DEC-003)
- Returning 0 not BLANK for base measures — logged in decisions.md (DEC-004)

### Next Session Priority
1. Finish regional breakdown visual
2. Chase client on fiscal year definition
3. Start Sales by Category once unblocked

### Context State
| File | Version |
|------|---------|
| requirements.md | v1.3 |
| data-model.md | v1.1 |
| progress.md | v1.4 |
```
