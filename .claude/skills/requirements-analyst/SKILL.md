---
name: requirements-analyst
description: Use this skill whenever the user wants to extract, structure, or update requirements from any raw input — call transcripts (VTT), emails, meeting notes, Excel files, or verbal descriptions. Trigger when the user mentions a client call, stakeholder meeting, or any raw notes that need to be turned into structured requirements. Also trigger when the user says "the client wants" or "we discussed" — don't wait for them to explicitly say "update requirements".
---

# Requirements Analyst

Extract, structure, and maintain requirements from raw inputs into `requirements.md`.

## Before Processing Any Input
1. Read existing `requirements.md` — avoid duplicates, detect conflicts
2. Read `decisions.md` — don't re-open decided matters
3. Read `data-model.md` — flag if required data doesn't exist yet

## Supported Input Types
| Input | Format | Notes |
|-------|--------|-------|
| Teams/Zoom transcript | `.vtt` | Ignore timestamps, extract content |
| Meeting notes | `.md` / `.txt` | Process as-is |
| Email content | pasted text | Strip signatures/headers |
| Excel file | `.xlsx` | Read tables and structured content |
| Verbal description | typed by user | Ask follow-up questions |

## VTT-Specific Rules
- Ignore all timestamp lines (`00:00:00.000 --> 00:00:00.000`)
- Ignore speaker labels unless ownership of request matters
- Focus on: decisions made, features requested, constraints, open questions
- Flag unclear items with ❓ — never guess
- One requirement per item — never bundle

## Extraction Rules
For every requirement, determine:
1. **Who** — which user role or stakeholder
2. **What** — the feature or metric requested
3. **Why** — what business decision it supports
4. **How** — calculation logic if mentioned
5. **Data** — tables/columns needed (cross-check with data-model.md)
6. **Gaps** — what's still unclear

## Output Format
```markdown
### REQ-[NNN]: [Short Name]
- **User Story**: As a [role], I want [feature] so that [outcome]
- **Acceptance Criteria**:
  - [ ] Criterion 1
  - [ ] Criterion 2
- **Data Dependencies**: `Table[Column]`, `[Measure Name]`
- **Priority**: High / Medium / Low
- **Source**: [call date / email / meeting]
- **Open Questions**:
  - ❓ Question 1
```

## Change Summary — Append After Every Update
```markdown
---
## Update Log: [YYYY-MM-DD] | v[X.X]
- ✅ Added: REQ-XXX, REQ-XXX
- ✏️ Modified: REQ-XXX — [what changed]
- ❓ Open Questions: [list]
- 🔴 Conflicts: [list]
- 📋 Source: [input file or description]
```

Read `references/examples.md` for full extraction examples before processing input.

## Self-Review Checklist
- [ ] No duplicate REQ numbers
- [ ] Every new REQ has at least 2 acceptance criteria
- [ ] Data dependencies cross-checked against data-model.md
- [ ] Conflicts flagged with 🔴
- [ ] Open questions listed — nothing assumed
- [ ] Change summary appended with version bump
- [ ] decisions.md checked — nothing re-opened
