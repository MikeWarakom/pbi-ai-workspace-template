# Data Model Examples

## Example 1 — Normalising a Flat Table

**Request**: "We have sales transactions with customer and product info mixed in"

**Proposed star schema**:

```markdown
### Proposed Model Change: Normalise Sales Flat Table

Current state: one flat Fact_Sales table with customer name, product name, category embedded

**Fact_Sales** (grain: one row per sales transaction)
| Column | Type | Role |
|--------|------|------|
| SalesKey | Integer | Surrogate PK |
| DateKey | Date | FK → Calendar |
| CustomerKey | Integer | FK → Dim_Customer |
| ProductKey | Integer | FK → Dim_Product |
| Amount | Decimal | Measure |
| Quantity | Integer | Measure |

**Dim_Customer** (grain: one row per customer)
| Column | Type | Role |
|--------|------|------|
| CustomerKey | Integer | Surrogate PK |
| CustomerName | String | Attribute |
| Region | String | Attribute |

**Dim_Product** (grain: one row per product)
| Column | Type | Role |
|--------|------|------|
| ProductKey | Integer | Surrogate PK |
| ProductName | String | Attribute |
| Category | String | Attribute |

Relationships:
- Fact_Sales[DateKey] → Calendar[Date] (Many-to-One, single)
- Fact_Sales[CustomerKey] → Dim_Customer[CustomerKey] (Many-to-One, single)
- Fact_Sales[ProductKey] → Dim_Product[ProductKey] (Many-to-One, single)

⚠️ Assumption: CustomerKey and ProductKey exist or will be added as surrogate keys in source
```

---

## Example 2 — Many-to-Many Resolution

**Request**: "Products can belong to multiple categories"

**Proposed bridge table**:

```markdown
### Proposed Model Change: Product-Category Many-to-Many

**Bridge_ProductCategory** (grain: one row per product-category combination)
| Column | Type | Role |
|--------|------|------|
| ProductKey | Integer | FK → Dim_Product |
| CategoryKey | Integer | FK → Dim_Category |

Relationships:
- Fact_Sales[ProductKey] → Dim_Product[ProductKey] (Many-to-One, single)
- Dim_Product[ProductKey] → Bridge_ProductCategory[ProductKey] (One-to-Many, single)
- Bridge_ProductCategory[CategoryKey] → Dim_Category[CategoryKey] (Many-to-One, single)

⚠️ Bidirectional filtering may be needed between Bridge and Dim_Category — document reason if applied
```
