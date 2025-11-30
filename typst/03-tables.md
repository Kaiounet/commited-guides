# Creating Tables in Typst

## Basic Table

```typst
#table(
  columns: 3,
  [Header 1], [Header 2], [Header 3],
  [Cell 1], [Cell 2], [Cell 3],
  [Cell 4], [Cell 5], [Cell 6],
)
```

This creates a 3-column table with 2 rows of data.

## Table with Borders

```typst
#table(
  columns: 2,
  stroke: 1pt + black,
  [Name], [Score],
  [Alice], [95],
  [Bob], [87],
  [Carol], [92],
)
```

## Header Row Styling

```typst
#table(
  columns: 3,
  stroke: (x, y) => (
    bottom: if y == 1 { 2pt } else { 0.5pt },
  ),
  fill: (x, y) => if y == 0 { rgb("#e0e0e0") },
  [Student], [Assignment 1], [Assignment 2],
  [Alice], [A], [A+],
  [Bob], [B], [B+],
)
```

## Complex Example

```typst
#table(
  columns: (1fr, 1fr, 1fr, auto),
  stroke: 1pt,
  align: (left, center, center, right),
  
  // Header
  [Feature], [Version 1], [Version 2], [Status],
  table.hline(),
  
  // Rows
  [Authentication], [No], [Yes], [✓ New],
  [API], [Basic], [REST], [✓ Updated],
  [Database], [SQLite], [PostgreSQL], [✓ New],
  [Testing], [Yes], [Yes], [- Same],
)
```

## Column Sizing

```typst
#table(
  columns: (1fr, 2fr, 1fr),  // 1:2:1 ratio
  [Small], [Medium (Double)], [Small],
  [A], [B], [C],
)

#table(
  columns: (100pt, 200pt, auto),  // Fixed sizes
  [100pt], [200pt], [Auto width],
  [Cell], [Cell], [Cell],
)
```

## Alignment

```typst
#table(
  columns: 3,
  align: (left, center, right),  // Per column
  [Left], [Center], [Right],
  [A], [B], [C],
)
```

## Colors in Tables

```typst
#table(
  columns: 3,
  fill: (x, y) => {
    if y == 0 { rgb("#4472C4") }  // Header row
    else if calc.rem(y, 2) == 0 { rgb("#D9E1F2") }  // Alternating rows
    else { white }
  },
  
  text(white)[Name],
  text(white)[Score],
  text(white)[Grade],
  
  [Alice], [95], [A],
  [Bob], [87], [B],
  [Carol], [92], [A],
)
```

## Tips

- Use `columns: 2` for 2-column table
- Use `1fr` for flexible width (fills available space)
- `stroke: 1pt + black` for borders
- `fill` lets you color cells
- `align` controls text alignment
- Use `table.hline()` to add horizontal lines
