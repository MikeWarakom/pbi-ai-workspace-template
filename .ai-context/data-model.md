# Data Model

## Model Overview
| Field | Value |
|-------|-------|
| Project | [Project Name] |
| Last Updated | [YYYY-MM-DD] |
| Schema Type | Star Schema / Mixed |
| Date Table | Calendar |

---

## Tables

### Table: Calendar
- **Type**: Dimension
- **Grain**: One row per day
- **Columns**:
  | Column | Type | Description |
  |--------|------|-------------|
  | Date | Date | Primary key |
  | Year | Integer | Calendar year |
  | Month | Integer | Month number 1-12 |
  | MonthName | String | January, February... |
  | Quarter | Integer | 1-4 |
  | WeekNumber | Integer | ISO week number |
  | IsWorkingDay | Boolean | Excludes weekends/holidays |
- **Relationships**: Connected to all date columns in fact tables
- **Notes**: Mark as Date Table in Power BI

---

<!-- COPY THIS BLOCK FOR EACH TABLE -->
### Table: [TableName]
- **Type**: Fact / Dimension / Bridge
- **Grain**: One row per [X]
- **Columns**:
  | Column | Type | Description |
  |--------|------|-------------|
  | [Column1] | Integer / String / Date / Decimal | [Description] |
- **Relationships**:
  - → `[RelatedTable][Key]` (Many-to-One, single direction)
- **Notes**: [Anything unusual about this table]

---

## Relationships Summary
| From Table | From Column | To Table | To Column | Cardinality | Direction |
|-----------|------------|---------|----------|------------|-----------|
| Fact_Sales | DateKey | Calendar | Date | Many-to-One | Single |
| Fact_Sales | CustomerKey | Dim_Customer | CustomerKey | Many-to-One | Single |

---

## Key Measures
List all measures here so AI has full context without reading the PBIX file.

| Measure | Table | Logic Summary |
|---------|-------|--------------|
| [Total Sales] | _Measures | SUM of Fact_Sales[Amount] |
| [Sales YTD] | _Measures | DATESYTD of [Total Sales] |

---

## Known Issues / Limitations
- [Data quality issue or model limitation]
- [Source system gap]
