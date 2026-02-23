# Documentation Examples

## Example — Sales YTD Measure

```markdown
## Sales YTD
**Version**: 1.0 | **Last Updated**: 2024-02-20

**Business Definition**
Shows the total sales revenue accumulated from the beginning of the calendar year
up to the most recent date visible in the report. Resets to zero on January 1st each year.

**Calculation Logic**
Takes the Total Sales measure and restricts it to only include dates from
January 1st of the current year through the currently selected date.

**DAX**
```dax
Sales YTD =
VAR LastVisibleDate =
    MAX(Calendar[Date])
VAR YTDSales =
    CALCULATE(
        [Total Sales],
        DATESYTD(Calendar[Date])
    )
RETURN
    IF(ISBLANK(YTDSales), 0, YTDSales)
```

**Dependencies**
- Tables: `Fact_Sales`, `Calendar`
- Measures: `[Total Sales]`
- Requires: Calendar marked as Date Table in Power BI

**Filter Behavior**
- Responds to: Date slicer, Region slicer, Product slicer
- Ignores: No filters removed — all context applies within the YTD window

**Edge Cases**
- Returns 0 (not BLANK) when no sales data exists for the period
- If Calendar is not marked as Date Table, DATESYTD will not work correctly

**Last Updated**: 2024-02-20 by Michal
```

---

## Example — Report Page Documentation

```markdown
## Page: Sales Overview

**Purpose**: Executive summary of sales performance for senior leadership
**Target Audience**: VP Sales, Regional Managers

**Key Visuals**
| Visual | Type | Question it answers |
|--------|------|-------------------|
| Total Sales KPI | Card | What is total sales this period? |
| Sales by Region | Bar chart | Which regions are performing best? |
| Sales vs Prior Year | Line chart | Are we growing vs last year? |

**Filters & Slicers**
- Date slicer: page-level, affects all visuals
- Region slicer: page-level, affects all visuals
- Product Category: visual-level on bar chart only

**Known Interactions**
- Clicking a region bar cross-filters the line chart
- Date slicer synced with Page 2 (Regional Detail)
```
