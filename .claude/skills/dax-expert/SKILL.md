---
name: dax-expert
description: Use this skill whenever the user needs to write, debug, or optimize DAX measures or calculated columns in Power BI. Trigger even if the user just mentions a metric, KPI, calculation, or business number they want to track — don't wait for them to explicitly ask for DAX code. Also trigger when the user asks about filter context, CALCULATE, time intelligence, or measure performance.
---

# DAX Expert

Write, debug, and optimize DAX measures and calculated columns in Power BI.
Before writing anything, read `references/examples.md` for output patterns.

## Mandatory Checks Before Writing
1. Confirm tables and columns exist in `data-model.md` — never invent names
2. Confirm the measure grain (one row = one what?)
3. Confirm filter context (which slicers/pages will affect this?)
4. Check `decisions.md` for any agreed calculation standards
5. If unclear — ask before writing

## DAX Best Practices

### Structure
- VAR / RETURN for every measure longer than 2 lines
- One VAR per logical step — name descriptively (not Var1, Var2)
- RETURN is always a single final expression

### Error Handling
- Always `DIVIDE(numerator, denominator, 0)` — never `/`
- Handle BLANK: `IF(ISBLANK([Measure]), 0, [Measure])` where needed
- Test mentally: no filters → one filter → all filters

### Filter Context
- Understand filter vs row context before using CALCULATE
- `REMOVEFILTERS()` over `ALL()` when intent is to clear filters
- `ALLEXCEPT()` over `FILTER(ALL(Table))` when possible
- `KEEPFILTERS()` when preserving existing context matters

### Performance
- Avoid SUMX/AVERAGEX when simple SUM/AVERAGE works
- Avoid FILTER on large tables — use column-level filters in CALCULATE
- Avoid deeply nested CALCULATE — split into VAR steps

## Naming Conventions
| Object | Convention | Example |
|--------|-----------|---------|
| Measures | Title Case, no prefix | `Sales YTD` |
| Helper measures | Underscore prefix | `_Sales Base` |
| Calculated columns | Title Case | `Full Name` |
| VARs | PascalCase, descriptive | `CurrentMonthSales` |

## Output Format — Always Use This Structure
```
-- ===========================
-- Measure: [Name]
-- Logic: [one-line plain English]
-- Dependencies: Table[Column], [Other Measure]
-- Edge cases: [what to watch for]
-- ===========================
[Measure Name] =
VAR [DescriptiveName] =
    [expression]
RETURN
    [final expression]
```

Then provide:
1. Plain-English explanation (non-technical)
2. Filter context assumptions
3. Suggested test cases

Read `references/examples.md` for full few-shot examples before writing.

## Self-Review Checklist
- [ ] All table/column names exist in `data-model.md`
- [ ] DIVIDE used — no `/` operator
- [ ] VAR/RETURN used for measures > 2 lines
- [ ] VARs named descriptively
- [ ] Comment block present
- [ ] Plain-English explanation included
- [ ] At least 2 test cases suggested
