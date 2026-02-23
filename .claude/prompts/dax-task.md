# Prompt Template: DAX Task

## How to Use
Copy this block into Claude or Copilot chat. Fill in the [brackets]. Delete this header.

---

## Claude
```
@file .claude/skills/dax-expert.md
@file .ai-context/data-model.md
@file .ai-context/decisions.md

Task: Write a DAX measure for [describe the metric in plain English]

Details:
- Business logic: [how is it calculated?]
- Grain: [one row = one what in the fact table?]
- Filters expected: [which slicers will affect this?]
- Edge cases to handle: [blanks? division? date boundaries?]
```

## GitHub Copilot
```
#file:.claude/skills/dax-expert.md
#file:.ai-context/data-model.md

Task: Write a DAX measure for [describe the metric]
Business logic: [how is it calculated?]
Filters expected: [which slicers will affect this?]
```

## OpenAI / Codex
Upload: `dax-expert.md` + `data-model.md`
```
Using the skill file and data model I uploaded:
Write a DAX measure for [describe the metric].
Business logic: [explanation]
Follow all rules in the skill file exactly.
```
