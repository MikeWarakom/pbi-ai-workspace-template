# Prompt Template: Code Review

## Claude
```
@file .claude/skills/code-reviewer.md
@file .ai-context/data-model.md
@file .ai-context/conventions.md
@file .ai-context/decisions.md

Please review the following [DAX measure / M query]:

[PASTE CODE HERE]

Context:
- What it should do: [plain English]
- Known concerns: [anything specific to check]
```

## GitHub Copilot
```
#file:.claude/skills/code-reviewer.md
#file:.ai-context/conventions.md
#file:.ai-context/data-model.md

Review this DAX measure:
[PASTE CODE HERE]

What it should do: [plain English]
```

## OpenAI / Codex
Upload: `code-reviewer.md` + `data-model.md` + `conventions.md`
```
Review the following DAX using the skill file and conventions I uploaded:
[PASTE CODE HERE]
```
