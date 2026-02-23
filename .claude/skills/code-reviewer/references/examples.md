# Code Review Examples

## Example 1 — Simple DAX issue
**Submitted**:
```dax
Profit Margin = [Total Profit] / [Total Sales]
```

**Review**:
```markdown
## Code Review: Profit Margin
**Date**: 2024-02-20

### 🔴 Issues (must fix)
- Division by zero risk: use `DIVIDE([Total Profit], [Total Sales], 0)`
- No VAR/RETURN — add for consistency
- No comment block

### Revised Code
-- ===========================
-- Measure: Profit Margin
-- Logic: Profit as % of sales, returns 0 if no sales
-- Dependencies: [Total Profit], [Total Sales]
-- Edge cases: Returns 0 when Total Sales is BLANK or zero
-- ===========================
Profit Margin =
VAR Margin =
    DIVIDE([Total Profit], [Total Sales], 0)
RETURN
    Margin
```

---

## Example 2 — Performance issue
**Submitted**:
```dax
Slow Sales =
SUMX(
    FILTER(Fact_Sales, Fact_Sales[Region] = "North"),
    Fact_Sales[Amount]
)
```

**Review**:
```markdown
## Code Review: Slow Sales
**Date**: 2024-02-20

### 🔴 Issues (must fix)
- FILTER on large fact table causes row-by-row iteration — use CALCULATE instead

### Revised Code
-- ===========================
-- Measure: North Region Sales
-- Logic: Sales filtered to North region using CALCULATE
-- Dependencies: Fact_Sales[Amount], Fact_Sales[Region]
-- Edge cases: Returns BLANK if no North region data
-- ===========================
North Region Sales =
VAR NorthSales =
    CALCULATE(
        SUM(Fact_Sales[Amount]),
        Fact_Sales[Region] = "North"
    )
RETURN
    NorthSales
```
