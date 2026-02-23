# Power BI AI Workspace Template — v2

A reusable, production-grade template for AI-enhanced Power BI development in VS Code.  
Works with **Claude**, **GitHub Copilot (free and paid)**, and **OpenAI / Codex**.

---

## What's New in v2
- ✅ **Session handoff file** — AI writes a handoff at end of each session, picks it up next time
- ✅ **Decisions log** — prevents AI from re-proposing settled decisions
- ✅ **Few-shot examples** in every skill — significantly improves output quality
- ✅ **Self-review checklists** in every skill — AI validates its own output before finishing
- ✅ **Ready-made prompt templates** — copy, fill in blanks, go
- ✅ **Version tracking** on all context files — know what changed and when

---

## Folder Structure

```
pbi-ai-workspace-template/
│
├── 📁 .github/
│   └── 📄 copilot-instructions.md       ⚡ auto-loaded by Copilot every session
│
├── 📁 .claude/
│   ├── 📄 CLAUDE.md                     ⚡ auto-loaded by Claude every session
│   ├── 📄 session-handoff.md            🔄 AI writes at end, you load at start
│   ├── 📁 skills/
│   │   ├── 📁 dax-expert/
│   │   │   ├── 📄 SKILL.md              🔵 DAX rules & instructions
│   │   │   └── 📁 references/
│   │   │       └── 📄 examples.md       📋 few-shot DAX examples
│   │   ├── 📁 requirements-analyst/
│   │   │   ├── 📄 SKILL.md              🔵 requirements extraction rules
│   │   │   └── 📁 references/
│   │   │       └── 📄 examples.md       📋 VTT & Excel extraction examples
│   │   ├── 📁 data-modeler/
│   │   │   ├── 📄 SKILL.md              🔵 star schema & model design rules
│   │   │   └── 📁 references/
│   │   │       └── 📄 examples.md       📋 model design examples
│   │   ├── 📁 code-reviewer/
│   │   │   ├── 📄 SKILL.md              🔵 DAX & M query review rules
│   │   │   └── 📁 references/
│   │   │       └── 📄 examples.md       📋 review examples
│   │   ├── 📁 documenter/
│   │   │   ├── 📄 SKILL.md              🔵 documentation writing rules
│   │   │   └── 📁 references/
│   │   │       └── 📄 examples.md       📋 documentation examples
│   │   └── 📁 progress-tracker/
│   │       ├── 📄 SKILL.md              🔵 progress & planning rules
│   │       └── 📁 references/
│   │           └── 📄 examples.md       📋 session update examples
│   └── 📁 prompts/
│       ├── 📄 dax-task.md               📋 copy-paste prompt for DAX tasks
│       ├── 📄 requirements-from-vtt.md  📋 copy-paste prompt for transcripts
│       ├── 📄 end-of-session.md         📋 copy-paste prompt for end of day
│       ├── 📄 code-review.md            📋 copy-paste prompt for reviews
│       └── 📄 data-model-update.md      📋 copy-paste prompt for model changes
│
└── 📁 .ai-context/
    ├── 📄 project.md                    🔧 fill once — overview & stakeholders
    ├── 📄 data-model.md                 🔄 keep updated — tables & columns
    ├── 📄 conventions.md                🔧 fill once — naming & formatting
    ├── 📄 decisions.md                  📝 log key decisions — AI reads before proposing
    ├── 📁 inputs/
    │   ├── 📄 README.md
    │   ├── 📄 YYYY-MM-DD-call.vtt       ⬇️ drop transcripts here
    │   └── 📄 YYYY-MM-DD-notes.md       ⬇️ drop meeting notes here
    └── 📁 outputs/
        ├── 📄 requirements.md           🤖 AI writes from inputs
        └── 📄 progress.md              🤖 AI updates each session
```

### Legend
```
⚡ auto-loaded    — always active, no action needed
🔵 skill file     — invoke with @file / #file: per task
🔧 fill once      — set up at project start, rarely changes
🔄 keep updated   — evolves as project progresses
📋 prompt template — copy, fill blanks, paste into chat
⬇️ drop here      — your raw inputs before each session
🤖 AI output      — AI writes, you paste and save
📝 you + AI       — both contribute over time
```

---

## Quick Start

1. Click **Use this template** on GitHub
2. Clone locally and open in VS Code
3. Fill in `.ai-context/project.md`
4. Fill in `.ai-context/data-model.md` after data discovery
5. Start your first session with the opener below

**First session opener (Claude)**:
```
@file .ai-context/project.md
@file .ai-context/data-model.md
@file .claude/session-handoff.md

This is a new project. Let's start with [first task].
```

---

## How to Use Each File

### Files You Fill In Once
| File | When | What |
|------|------|------|
| `.ai-context/project.md` | Project start | Name, client, scope, stakeholders |
| `.ai-context/data-model.md` | After data discovery | Tables, columns, relationships |
| `.ai-context/conventions.md` | Project start | Naming rules, DAX standards |

### Files That Grow Over Time
| File | Updated by | When |
|------|-----------|------|
| `.ai-context/decisions.md` | You + AI | Any time a key decision is made |
| `.claude/session-handoff.md` | AI | End of every session |
| `.ai-context/outputs/requirements.md` | AI | After each call or meeting |
| `.ai-context/outputs/progress.md` | AI | End of each work session |

### How to Save AI Output
1. AI outputs the full updated file content
2. Open the target file in VS Code
3. Select all (`Ctrl+A`) → Paste → Save (`Ctrl+S`)
4. Commit: `git commit -m "docs: update requirements from 2024-02-20 call"`

**Always replace the full file** — never partially update to avoid inconsistencies.

### Files You Drop Before Sessions
Save inputs in `.ai-context/inputs/` with naming: `YYYY-MM-DD-description.ext`

---

## Session Workflow

### Start of Session
```
@file .ai-context/project.md
@file .claude/session-handoff.md
@file .ai-context/data-model.md

Continuing from last session. Today I want to [task].
```

### During Session — Use Prompt Templates
Open the relevant file from `.claude/prompts/` and copy the block for your tool.

### End of Session
Open `.claude/prompts/end-of-session.md` and run the end-of-session prompt.
Save both outputs: `progress.md` and prepend the handoff block to `session-handoff.md`.

---

## Prompt Templates Quick Reference

| Task | Template file |
|------|-------------|
| Write a DAX measure | `.claude/prompts/dax-task.md` |
| Process a call transcript | `.claude/prompts/requirements-from-vtt.md` |
| End of day update | `.claude/prompts/end-of-session.md` |
| Review existing DAX | `.claude/prompts/code-review.md` |
| Update data model | `.claude/prompts/data-model-update.md` |

---

## Tool Comparison

| Feature | Claude | Copilot Free | OpenAI / Codex |
|---------|--------|-------------|----------------|
| Auto-loads instructions | ✅ CLAUDE.md | ✅ copilot-instructions.md | ❌ upload each session |
| File references | `@file` | `#file:` | upload files |
| Multi-file in one prompt | ✅ | ⚠️ split into steps | ✅ upload all |
| Best for DAX | Sonnet ✅ | GPT-4o | gpt-4 |
| Best for requirements | Opus ✅ | GPT-4o | gpt-4 |
| Best for progress | Haiku ✅ | GPT-3.5 | gpt-3.5-turbo |

---

## Replicating to a New Project

1. **Use this template** on GitHub → clone locally
2. Fill in `project.md` (30 min)
3. Fill in `data-model.md` after data discovery session (1-2 hrs)
4. Clear `outputs/requirements.md` and `outputs/progress.md` (keep structure, delete example content)
5. Clear `decisions.md` (keep structure)
6. Clear `session-handoff.md` (keep structure)
7. First commit: `git commit -m "feat: project setup complete"`

---

## Tips
- **`decisions.md` is your most underrated file** — every time you agree something with a client, log it. AI won't re-propose it and you won't forget it.
- **Always load `data-model.md` for DAX** — this single habit prevents 90% of AI column-name mistakes
- **Commit after every AI session** — your context files are living documentation and git is your history
- **Prompt templates save you 2-3 minutes per task** — over a project that adds up

---

## MCP Integration — Power BI Modeling MCP Server

For a fully agentic setup where AI writes directly into your Power BI model
(instead of you copy-pasting DAX), install the official Microsoft MCP server.

See **[mcp-setup.md](mcp-setup.md)** for full setup instructions.

### What MCP Changes
```
Without MCP:
AI suggests DAX → you copy → you paste into Power BI Desktop

With MCP:
AI writes DAX directly into your live model → you approve → done
```

### Impact on Template Files
| File | Without MCP | With MCP |
|------|------------|---------|
| `data-model.md` | You maintain manually | Auto-generate from live model |
| `skills/dax-expert.md` | AI follows rules, outputs text | AI follows rules, writes directly |
| `session-handoff.md` | Same | Same — MCP has no memory |
| `decisions.md` | Same | Same — MCP doesn't know what was agreed |

> ⚠️ MCP is in Public Preview. Always back up your model before write operations.  
> GitHub repo: https://github.com/microsoft/powerbi-modeling-mcp
