---
name: code-reviewer
description: Use this skill whenever the user wants existing DAX measures, M queries, or Power BI model decisions reviewed. Trigger when the user pastes code and asks "is this right", "can you check this", "what's wrong with this", or shares a measure they wrote themselves. Also trigger when the user mentions performance issues with existing measures.
---

# Code Reviewer

Review DAX measures, M queries, and Power BI model decisions for correctness,
performance, maintainability, and adherence to project conventions.

## Before Reviewing
1. Read `conventions.md` — review against project standards, not generic ones
2. Read `data-model.md` — verify column/table references exist
3. Read `decisions.md` — flag if code contradicts agreed decisions

## DAX Review Checklist
- [ ] VAR/RETURN used for measures > 2 lines
- [ ] DIVIDE() used — no `/` operator
- [ ] BLANK handled where needed
- [ ] No hardcoded values (dates, IDs) — use dynamic references
- [ ] CALCULATE used correctly — filter vs row context understood
- [ ] No FILTER(ALL(Table)) where ALLEXCEPT is more precise
- [ ] VARs named descriptively
- [ ] Comment block present above measure
- [ ] Naming follows `conventions.md`
- [ ] No unnecessary row-by-row iteration (SUMX/AVERAGEX overuse)

## M Query Checklist
- [ ] Steps named descriptively
- [ ] No hardcoded file paths or credentials
- [ ] Data types explicitly set
- [ ] Unnecessary columns removed early
- [ ] Error handling for source connectivity

## Model Checklist
- [ ] Star schema maintained
- [ ] No bidirectional relationships without documented reason
- [ ] Calendar marked as Date Table
- [ ] Foreign key columns hidden from report view
- [ ] No calculated columns that should be measures

## Output Format
```markdown
## Code Review: [Name]
**Date**: [YYYY-MM-DD]

### ✅ Passed
- [what is correct]

### ⚠️ Suggestions (optional improvement)
- [improvement, not breaking]

### 🔴 Issues (must fix)
- [correctness or performance problem]

### Revised Code
[corrected version]
```

Read `references/examples.md` for full review examples.

## Self-Review Checklist
- [ ] Checked against conventions.md, not just generic rules
- [ ] All column/table names verified against data-model.md
- [ ] decisions.md checked for conflicts
- [ ] Revised code provided for every 🔴 issue
