# Prompt Template: Requirements from VTT Transcript

## How to Use
Save your transcript as `.ai-context/inputs/YYYY-MM-DD-[description].vtt` first.
Then copy the relevant block below into your AI chat.

---

## Claude (single step)
```
@file .claude/skills/requirements-analyst.md
@file .ai-context/outputs/requirements.md
@file .ai-context/data-model.md
@file .ai-context/decisions.md
@file .ai-context/inputs/[YYYY-MM-DD-filename].vtt

The last file is a Teams/Zoom call transcript in VTT format.
Ignore timestamps and speaker labels — extract content only.
Update requirements.md with any new or changed requirements.
Flag conflicts with existing requirements.
Flag any requirements that need data not in data-model.md.
Output the full updated requirements.md ready to save.
```

## GitHub Copilot Free (two steps)

Step 1 — Extract:
```
#file:.claude/skills/requirements-analyst.md
#file:.ai-context/inputs/[YYYY-MM-DD-filename].vtt

This is a VTT transcript. Ignore timestamps and speaker labels.
Extract all requirements using the skill file format.
```

Step 2 — Merge (paste Step 1 output below):
```
#file:.ai-context/outputs/requirements.md

Merge the requirements below into the existing file.
No duplicates. Flag conflicts. Output full updated file ready to save.

[PASTE STEP 1 OUTPUT HERE]
```

## OpenAI / Codex
Upload: `requirements-analyst.md` + `requirements.md` + your `.vtt` file
```
Using the three files I uploaded:
Extract requirements from the VTT transcript.
Merge into the existing requirements.md without duplicates.
Follow the skill file format exactly.
Output the full updated requirements.md.
```
