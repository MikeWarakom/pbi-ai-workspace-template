# Prompt Template: End of Session

## How to Use
Run this at the end of every work session. Fill in what you completed.

---

## Claude
```
@file .claude/skills/progress-tracker.md
@file .ai-context/outputs/progress.md
@file .ai-context/outputs/requirements.md
@file .claude/session-handoff.md

Today I completed:
- [task 1]
- [task 2]

Still in progress:
- [task] — current state: [where you left off]

Blockers:
- [blocker] — waiting on: [what/who]

Please:
1. Output the full updated progress.md ready to save
2. Output a session-handoff.md block to prepend to the handoff file
```

## GitHub Copilot
```
#file:.claude/skills/progress-tracker.md
#file:.ai-context/outputs/progress.md

Today I completed: [list]
Still in progress: [list with current state]
Blockers: [list]

Output the full updated progress.md ready to save.
Then write a session summary I can add to my handoff file.
```
