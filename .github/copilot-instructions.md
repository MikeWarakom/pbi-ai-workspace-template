# GitHub Copilot Workspace Instructions — v2
# Power BI Development — AI-Enhanced Workflow

## Session Start Protocol
1. Read `#file:.ai-context/project.md`
2. Read `#file:.claude/session-handoff.md` — continue from last session
3. Read `#file:.ai-context/data-model.md` before any DAX work
4. Confirm task with user before starting

## Always Do
- Use only table/column names from `data-model.md` — never invent names
- Follow conventions in `conventions.md`
- Check `decisions.md` before proposing anything — don't re-open settled decisions
- Flag assumptions with ⚠️ and risks with 🔴
- Output full file content when updating any context file
- Append change summary + version bump to updated files

## Never Do
- Invent table or column names
- Use `/` for division — always `DIVIDE()`
- Skip error handling in DAX
- Bundle multiple requirements into one
- Guess when context is missing — ask for the file

## Available Skills — use #file: to load

| Task | Load |
|------|------|
| DAX writing | `#file:.claude/skills/dax-expert.md` + `#file:.ai-context/data-model.md` |
| Requirements | `#file:.claude/skills/requirements-analyst.md` + `#file:.ai-context/outputs/requirements.md` |
| Data model | `#file:.claude/skills/data-modeler.md` + `#file:.ai-context/data-model.md` |
| Code review | `#file:.claude/skills/code-reviewer.md` + `#file:.ai-context/conventions.md` |
| Documentation | `#file:.claude/skills/documenter.md` |
| Progress | `#file:.claude/skills/progress-tracker.md` + `#file:.ai-context/outputs/progress.md` |

## Prompt Templates
Ready-made prompts in `.claude/prompts/` — copy and fill in the Copilot section for each task.
