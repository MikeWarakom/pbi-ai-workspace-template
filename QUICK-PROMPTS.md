# AI Quick Prompts — Power BI Workspace
> Copy, fill in the blanks, paste into Claude Code / Copilot / Cursor

---

## 🔵 DAX Expert

### Write a new measure
```
@.claude/skills/dax-expert/SKILL.md
@.claude/skills/dax-expert/references/examples.md
@.ai-context/data-model.md
@.ai-context/decisions.md

Write a [measure name] measure.
Logic: [describe what it should calculate]
Table: [Fact_TableName]
Column: [ColumnName]
```

### Debug an existing measure
```
@.claude/skills/dax-expert/SKILL.md
@.claude/skills/dax-expert/references/examples.md
@.ai-context/data-model.md

Debug this measure — it returns [wrong result / blank / error]:

[paste DAX here]
```

### Write a time intelligence measure
```
@.claude/skills/dax-expert/SKILL.md
@.claude/skills/dax-expert/references/examples.md
@.ai-context/data-model.md

Write [YTD / MTD / Prior Year / Rolling 3M] version of this measure:

[paste base measure here]
```

---

## 📋 Requirements Analyst

### Process a VTT transcript
```
@.claude/skills/requirements-analyst/SKILL.md
@.claude/skills/requirements-analyst/references/examples.md
@.ai-context/outputs/requirements.md
@.ai-context/data-model.md
@.ai-context/decisions.md
@.ai-context/inputs/[YYYY-MM-DD-filename.vtt]

Process the VTT transcript. Extract all requirements, update requirements.md,
append the change summary. Output the full updated file ready to save.
```

### Process an Excel or meeting notes file
```
@.claude/skills/requirements-analyst/SKILL.md
@.claude/skills/requirements-analyst/references/examples.md
@.ai-context/outputs/requirements.md
@.ai-context/data-model.md
@.ai-context/inputs/[filename.xlsx or filename.md]

Extract requirements from the input file. Update requirements.md.
Flag any data gaps against data-model.md. Output full updated file.
```

### Add a single verbal requirement
```
@.claude/skills/requirements-analyst/SKILL.md
@.ai-context/outputs/requirements.md
@.ai-context/data-model.md

Add this requirement from today's call:
[describe what the client asked for]
Source: [who said it / when]
```

---

## 🗂️ Data Modeler

### Review and propose model changes
```
@.claude/skills/data-modeler/SKILL.md
@.claude/skills/data-modeler/references/examples.md
@.ai-context/data-model.md
@.ai-context/requirements.md
@.ai-context/decisions.md

Review the current data model against requirements.
Propose any structural changes needed. Follow star schema principles.
```

### Add a new table to the model
```
@.claude/skills/data-modeler/SKILL.md
@.ai-context/data-model.md

Add this new table to data-model.md:
Table name: [name]
Source: [where the data comes from]
Columns available: [list columns]
How it relates to existing tables: [describe]
```

### Generate data-model.md from live model (MCP)
```
@.claude/skills/data-modeler/SKILL.md
@.ai-context/data-model.md

Connect to '[filename]' in Power BI Desktop.
Read the full semantic model structure and update data-model.md
to reflect the current state. Follow the existing format.
```

---

## 🔍 Code Reviewer

### Review a DAX measure
```
@.claude/skills/code-reviewer/SKILL.md
@.claude/skills/code-reviewer/references/examples.md
@.ai-context/conventions.md
@.ai-context/data-model.md
@.ai-context/decisions.md

Review this DAX measure:

[paste DAX here]
```

### Review all measures in a file
```
@.claude/skills/code-reviewer/SKILL.md
@.claude/skills/code-reviewer/references/examples.md
@.ai-context/conventions.md
@.ai-context/data-model.md
@[path-to-measures-file]

Review all measures in the attached file.
Flag issues by severity: 🔴 must fix / ⚠️ suggestion / ✅ passed.
```

---

## 📝 Documenter

### Document a single measure
```
@.claude/skills/documenter/SKILL.md
@.claude/skills/documenter/references/examples.md
@.ai-context/data-model.md
@.ai-context/conventions.md

Document this measure for the technical handover pack:

[paste DAX here]
```

### Document all measures in a table
```
@.claude/skills/documenter/SKILL.md
@.claude/skills/documenter/references/examples.md
@.ai-context/data-model.md

Document all measures in the [table name] measures table.
Use the standard measure documentation template.
```

---

## 📊 Progress Tracker

### End of session update
```
@.claude/skills/progress-tracker/SKILL.md
@.claude/skills/progress-tracker/references/examples.md
@.ai-context/outputs/progress.md
@.ai-context/outputs/requirements.md
@.claude/session-handoff.md

Today I completed: [list what you finished]
Still in progress: [list what's ongoing]
Blockers: [anything stuck and why]

Update progress.md, append session log, and produce the session-handoff.md block.
```

### Check what to work on next
```
@.claude/skills/progress-tracker/SKILL.md
@.ai-context/outputs/progress.md
@.ai-context/outputs/requirements.md

Based on current progress and requirements, what are the top 3 priorities
for this session? Consider blockers and dependencies.
```

---

## 🚀 Session Starter

### Load context at start of session
```
@.claude/CLAUDE.md
@.claude/session-handoff.md
@.ai-context/project.md
@.ai-context/data-model.md
@.ai-context/decisions.md

Continue from last session. Summarise where we left off and confirm
the top priority for today.
```

---

## 💡 Tips

- **Claude Code**: use `@filename` syntax
- **GitHub Copilot**: use `#file:filename` syntax  
- **Cursor**: use `@filename` syntax
- Always include `data-model.md` for any DAX or model task
- Always include `decisions.md` to avoid re-opening agreed matters
- Load `examples.md` for complex tasks, skip it for simple ones to save context
