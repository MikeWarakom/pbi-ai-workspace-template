# Conventions & Standards

## DAX Naming
| Object | Convention | Example |
|--------|-----------|---------|
| Measures | Title Case, no prefix | `Sales YTD` |
| Hidden helper measures | Underscore prefix | `_Sales Base` |
| Calculated columns | Title Case | `Full Name` |

## Table Naming
| Object | Convention | Example |
|--------|-----------|---------|
| Fact tables | `Fact_[Name]` | `Fact_Sales` |
| Dimension tables | `Dim_[Name]` | `Dim_Customer` |
| Bridge tables | `Bridge_[Name]` | `Bridge_ProductCategory` |
| Date table | `Calendar` | `Calendar` |
| Measures table | `_Measures` | `_Measures` |

## DAX Formatting
- Always use VAR / RETURN for measures > 2 lines
- Always use DIVIDE() — never `/`
- One VAR per logical step
- Indentation: 4 spaces
- Comment block required above every measure

## M Query Standards
- Name every step descriptively
- Remove unused columns early
- Set data types explicitly on every column
- No hardcoded file paths

## Report Standards
- [Color palette, font standards if applicable]
- [Page naming convention]
- [Tooltip standards]

## Version Control
- Commit message format: `[type]: [short description]`
- Types: `feat`, `fix`, `docs`, `refactor`, `data`
- Example: `feat: add YTD sales measure`
