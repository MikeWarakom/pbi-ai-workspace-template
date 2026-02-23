# Requirements Extraction Examples

## Example 1 — From VTT line to requirement
**Raw VTT**:
```
00:04:32.000 --> 00:04:45.000
Client: We need to see sales broken down by region, and compare it to last year
```

**Extracted**:
```markdown
### REQ-004: Regional Sales with Prior Year Comparison
- **User Story**: As a sales manager, I want to see sales by region vs prior year so that I can identify underperforming regions
- **Acceptance Criteria**:
  - [ ] Visual shows current year sales by region
  - [ ] Prior year value shown alongside for comparison
  - [ ] Variance (absolute and %) also displayed
- **Data Dependencies**: `Fact_Sales[Amount]`, `Dim_Region[RegionName]`, `Calendar[Date]`
- **Priority**: High
- **Source**: kickoff-call-2024-02-20.vtt (00:04:32)
- **Open Questions**:
  - ❓ Which regions — country level or sub-region?
  - ❓ Calendar year or fiscal year comparison?
```

---

## Example 2 — Conflicting requirement
**Raw input**: "Finance wants YTD, but the sales team said they only want monthly"

**Extracted**:
```markdown
### REQ-008: Sales Time Period Selection
- **User Story**: As a report user, I want to choose between YTD and monthly views
- **Acceptance Criteria**:
  - [ ] Toggle or slicer allows switching between Monthly and YTD
- **Data Dependencies**: `[Total Sales]`, `[Sales YTD]`, `Calendar[Date]`
- **Priority**: High
- **Source**: requirements-email-2024-02-21.md
- **Open Questions**:
  - ❓ Should this be a page-level toggle or report-level?
- 🔴 **Conflict**: Finance (YTD) vs Sales team (Monthly) — needs stakeholder alignment before build
```

---

## Example 3 — From Excel data dictionary
**Raw input**: Excel with columns: Product, Region, SalesRep, Amount, Date

**Extracted**:
```markdown
### REQ-012: Sales Data Grain Confirmation
- **User Story**: As a developer, I want to confirm the data grain so that measures are built correctly
- **Acceptance Criteria**:
  - [ ] One row = one sale transaction confirmed with client
  - [ ] All dimension columns confirmed as attributes not measures
- **Data Dependencies**: `Fact_Sales[Amount]`, `Dim_Product`, `Dim_Region`
- **Priority**: High
- **Source**: data-dictionary.xlsx
- **Open Questions**:
  - ❓ Is SalesRep a dimension or just an attribute on the fact?
  - ❓ Is Date the transaction date or the posting date?
```

---

## Change Summary Example
```markdown
---
## Update Log: 2024-02-20 | v1.3
- ✅ Added: REQ-004, REQ-008, REQ-012
- ✏️ Modified: REQ-001 — updated acceptance criteria to include mobile view
- ❓ Open Questions: fiscal year definition, sub-region level, SalesRep grain
- 🔴 Conflicts: REQ-008 Finance vs Sales team — escalate to project manager
- 📋 Source: kickoff-call-2024-02-20.vtt
```
