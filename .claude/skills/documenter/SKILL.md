---
name: documenter
description: Use this skill whenever the user needs to write or update technical documentation for Power BI measures, report pages, or data sources. Trigger when the user says "document this", "write a description", "explain what this measure does", or when preparing handover material. Also trigger when adding descriptions to measures in bulk.
---

# Documenter

Write clear, consistent technical documentation for Power BI measures,
report pages, and data sources.

## Before Writing
1. Read existing documentation to match style and version
2. Read `data-model.md` for accurate technical details
3. Read `conventions.md` for naming and formatting standards

## Documentation Types

### Measure Documentation
- Business definition — plain English, no DAX syntax
- Technical logic — step-by-step without code
- DAX code block
- Dependencies (tables, columns, other measures)
- Filter context behavior
- Edge cases and known limitations

### Report Page Documentation
- Page purpose and target audience
- Key visuals and what questions they answer
- Filters, slicers, and their scope
- Visual interactions

## Output Template — Measure
```markdown
## [Measure Name]
**Version**: [X.X] | **Last Updated**: [YYYY-MM-DD]

**Business Definition**
[Plain English — what does this number mean to a business user?]

**Calculation Logic**
[Step-by-step without DAX syntax]

**DAX**
```dax
[code]
```

**Dependencies**
- Tables: `Table1`
- Measures: `[Base Measure]`

**Filter Behavior**
- Responds to: [list of slicers/filters]
- Ignores: [any filters removed]

**Edge Cases**
- [condition]: [what happens]

**Last Updated**: [YYYY-MM-DD] by [name]
```

Read `references/examples.md` for full documentation examples.

## Self-Review Checklist
- [ ] Business definition uses no DAX or technical jargon
- [ ] Technical details accurate against data-model.md
- [ ] All dependencies listed
- [ ] At least one edge case documented
- [ ] Version and date updated
