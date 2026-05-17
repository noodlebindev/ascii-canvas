# comparison-table

## Purpose

Side-by-side comparison of 2–5 options across a shared set of dimensions.

## Use when

- Evaluating choices between two or more options
- Pros/cons across multiple frameworks, tools, or approaches
- Feature comparison where readers need to pick one option
- Structured trade-off analysis that doesn't need narrative

## Do NOT use when

- Narrative trade-off discussion is needed — use `slideshow`
- Single option deep-dive — use `cheat-sheet`

## Width budget

100 cols

## Arc

N/A — single artifact

## Layout rules

- Header row: option names across columns
- Leftmost column: dimensions (row labels)
- Use ✓ / ✗ / ~ for quick categorical values; prose for nuanced cells
- Equal-width option columns when option count is even
- Dimension column width = longest dimension label + 2 padding chars

## Canonical skeleton — Unicode

```
┌──────────────────────┬─────────────────┬─────────────────┬─────────────────┐
│ Dimension            │   Option A      │   Option B      │   Option C      │
├──────────────────────┼─────────────────┼─────────────────┼─────────────────┤
│ <Dimension 1>        │ <value>         │ <value>         │ <value>         │
│ <Dimension 2>        │      ✓          │      ✗          │      ~          │
│ <Dimension 3>        │ <value>         │ <value>         │ <value>         │
└──────────────────────┴─────────────────┴─────────────────┴─────────────────┘
```

## Canonical skeleton — ASCII fallback

```
+----------------------+-----------------+-----------------+-----------------+
| Dimension            |   Option A      |   Option B      |   Option C      |
+----------------------+-----------------+-----------------+-----------------+
| <Dimension 1>        | <value>         | <value>         | <value>         |
| <Dimension 2>        |       Y         |       N         |       ~         |
| <Dimension 3>        | <value>         | <value>         | <value>         |
+----------------------+-----------------+-----------------+-----------------+
```

## Short rendered example

```
PostgreSQL vs MySQL vs SQLite

┌──────────────────────┬─────────────────┬─────────────────┬─────────────────┐
│ Dimension            │   PostgreSQL    │     MySQL       │     SQLite      │
├──────────────────────┼─────────────────┼─────────────────┼─────────────────┤
│ Schema flexibility   │ High (JSONB)    │ Medium          │ Low             │
│ Replication          │      ✓          │      ✓          │      ✗          │
│ Embedded use         │      ✗          │      ✗          │      ✓          │
│ Full-text search     │      ✓          │      ~          │      ~          │
└──────────────────────┴─────────────────┴─────────────────┴─────────────────┘
```

## Failure modes

- If options exceed 5 → reduce number of dimensions or split into themed sub-tables
- If dimensions need narrative explanation → fall back to `slideshow`
- If table width overflows at 100 cols → shorten option/dimension labels or drop to 2 options
