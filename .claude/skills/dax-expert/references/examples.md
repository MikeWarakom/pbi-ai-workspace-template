# DAX Examples Reference

## Example 1 — Simple measure with error handling
**Request**: Total sales amount, handle blanks

```dax
-- ===========================
-- Measure: Total Sales
-- Logic: Sum of all sales amounts, returns 0 if no data
-- Dependencies: Fact_Sales[Amount]
-- Edge cases: Returns 0 (not BLANK) when no rows match
-- ===========================
Total Sales =
VAR SalesAmount =
    SUM(Fact_Sales[Amount])
RETURN
    IF(ISBLANK(SalesAmount), 0, SalesAmount)
```

---

## Example 2 — Time intelligence with VAR/RETURN
**Request**: Year-to-date sales

```dax
-- ===========================
-- Measure: Sales YTD
-- Logic: Cumulative sales from Jan 1 to current filtered date
-- Dependencies: Fact_Sales[Amount], Calendar[Date]
-- Edge cases: Requires Calendar marked as Date Table
-- ===========================
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

---

## Example 3 — Prior year comparison
**Request**: Prior year sales for same period

```dax
-- ===========================
-- Measure: Sales PY
-- Logic: Sales for the same period one year ago
-- Dependencies: [Total Sales], Calendar[Date]
-- Edge cases: Returns BLANK if no prior year data (intentional for charts)
-- ===========================
Sales PY =
VAR PriorYearSales =
    CALCULATE(
        [Total Sales],
        SAMEPERIODLASTYEAR(Calendar[Date])
    )
RETURN
    PriorYearSales
```

---

## Example 4 — Ratio with safe division
**Request**: Profit margin percentage

```dax
-- ===========================
-- Measure: Profit Margin %
-- Logic: Profit as % of sales, returns 0 if no sales
-- Dependencies: [Total Profit], [Total Sales]
-- Edge cases: Returns 0 when Total Sales is BLANK or zero
-- ===========================
Profit Margin % =
VAR Margin =
    DIVIDE([Total Profit], [Total Sales], 0)
RETURN
    Margin
```

---

## Example 5 — Rolling average
**Request**: 3-month rolling average sales

```dax
-- ===========================
-- Measure: Sales 3M Rolling Avg
-- Logic: Average monthly sales over last 3 months
-- Dependencies: [Total Sales], Calendar[Date]
-- Edge cases: Returns BLANK if fewer than 3 months of data
-- ===========================
Sales 3M Rolling Avg =
VAR LastDate =
    MAX(Calendar[Date])
VAR RollingWindow =
    DATESINPERIOD(Calendar[Date], LastDate, -3, MONTH)
VAR RollingTotal =
    CALCULATE([Total Sales], RollingWindow)
VAR MonthCount =
    CALCULATE(DISTINCTCOUNT(Calendar[Month]), RollingWindow)
RETURN
    DIVIDE(RollingTotal, MonthCount, BLANK())
```
