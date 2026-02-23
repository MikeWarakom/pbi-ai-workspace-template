---
name: data-modeler
description: Use this skill whenever the user needs to design, review, or document a Power BI data model. Trigger when the user mentions tables, relationships, star schema, fact tables, dimension tables, grain, or asks how to structure their data. Also trigger when new data sources are being added or when the user says the model feels slow or has relationship issues.
---

# Data Modeler

Design, review, and document Power BI data models following star schema best practices.

## Before Designing
1. Read `data-model.md` — understand what already exists
2. Read `requirements.md` — understand what data the reports need
3. Read `decisions.md` — check for agreed modelling decisions

## Core Principles

### Star Schema First
- Fact tables: transactional data, numeric measures, foreign keys only
- Dimension tables: descriptive attributes, surrogate keys, no measures
- Always prefer star over flat or snowflake where possible
- Resolve many-to-many with bridge tables — never leave them implicit

### Grain Definition (mandatory)
- Every fact table needs: "One row = one [X]"
- Document grain explicitly — all measures must be consistent with it

### Relationships
- Single-direction by default — document any bidirectional exceptions
- Always connect every date column in facts to Calendar dimension
- Avoid ambiguous relationship paths

### Performance
- Hide foreign key columns from report view
- Mark Calendar as Date Table
- Avoid calculated columns where measures can replace them
- Keep dimension tables narrow

## Naming Conventions
| Object | Convention | Example |
|--------|-----------|---------|
| Fact tables | `Fact_[Name]` | `Fact_Sales` |
| Dimension tables | `Dim_[Name]` | `Dim_Customer` |
| Bridge tables | `Bridge_[Name]` | `Bridge_ProductCategory` |
| Date table | `Calendar` | `Calendar` |
| Measures table | `_Measures` | `_Measures` |
| Surrogate keys | `[Table]Key` | `CustomerKey` |

## data-model.md Update Format
```markdown
### Table: [TableName]
- **Type**: Fact / Dimension / Bridge / Calendar
- **Grain**: One row per [X]
- **Columns**:
  | Column | Type | Description |
  |--------|------|-------------|
  | [Column] | Integer / String / Date / Decimal | [Description] |
- **Relationships**:
  - → `[RelatedTable][Key]` (Many-to-One, single direction)
- **Notes**: [anything unusual]
```

Read `references/examples.md` for full star schema design examples.

## Self-Review Checklist
- [ ] Grain defined for every fact table
- [ ] No many-to-many left unresolved
- [ ] All date columns connected to Calendar
- [ ] Foreign keys hidden from report view in proposal
- [ ] decisions.md checked — no conflicts with agreed model direction
