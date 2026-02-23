# Claude Workspace Instructions — v2
# Power BI Development — AI-Enhanced Workflow

---

## Session Start Protocol (always follow this order)
1. Read `.ai-context/project.md` — understand project scope and stakeholders
2. Read `.claude/session-handoff.md` — pick up where the last session left off
3. Read `.ai-context/data-model.md` — know the tables and columns before any DAX
4. Confirm task with user before starting work

---

## Always Do
- Read `data-model.md` before writing ANY DAX — never invent table or column names
- Follow naming conventions in `.ai-context/conventions.md`
- Cross-reference `decisions.md` before proposing anything that may already be decided
- Ask clarifying questions if requirements are ambiguous before producing output
- Explain the *why* behind every suggestion, not just the what
- Flag assumptions with ⚠️ and breaking changes or risks with 🔴
- Output updated file content in full when asked to update any context file
- Append a change summary + version bump when updating any context file
- Write a session handoff update at the end of every session

## Never Do
- Invent table or column names not found in `data-model.md`
- Skip BLANK/DIVIDE error handling in DAX
- Bundle multiple requirements into a single requirement item
- Guess when context is missing — ask for the right file instead
- Re-propose something already decided in `decisions.md` without flagging the conflict

## Response Format
- Code blocks for all DAX, M query, SQL, JSON
- Markdown tables for comparisons or options
- Concise explanations unless asked to elaborate
- Change summary appended when updating any context file

---

## Available Skills — Load per Task

| Task | Claude Invoke | Model |
|------|--------------|-------|
| Write or debug DAX | `@file .claude/skills/dax-expert.md` + `@file .ai-context/data-model.md` | Sonnet |
| Requirements from call/notes | `@file .claude/skills/requirements-analyst.md` + `@file .ai-context/outputs/requirements.md` | Opus |
| Data model design | `@file .claude/skills/data-modeler.md` + `@file .ai-context/data-model.md` | Sonnet |
| Code review | `@file .claude/skills/code-reviewer.md` + `@file .ai-context/conventions.md` | Sonnet |
| Documentation | `@file .claude/skills/documenter.md` | Sonnet |
| Progress update | `@file .claude/skills/progress-tracker.md` + `@file .ai-context/outputs/progress.md` | Haiku |
| Process VTT transcript | `@file .claude/skills/requirements-analyst.md` + `@file .ai-context/outputs/requirements.md` + `@file .ai-context/inputs/[file].vtt` | Opus |

---

## Ready-Made Prompt Templates

| Task | Template |
|------|---------|
| DAX measure | `@file .claude/prompts/dax-task.md` |
| Requirements from VTT | `@file .claude/prompts/requirements-from-vtt.md` |
| End of session | `@file .claude/prompts/end-of-session.md` |
| Code review | `@file .claude/prompts/code-review.md` |
| Data model update | `@file .claude/prompts/data-model-update.md` |

---

## Session Handoff Protocol
At the end of every session, update `.claude/session-handoff.md` with:
- What was completed this session
- What is in progress and its current state
- Open questions or blockers
- Recommended focus for next session
