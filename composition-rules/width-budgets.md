# Width budgets

Every format has a defined max column width. Never exceed it.

## Per-format budgets

| Format | Max width (cols) |
|---|---|
| slideshow | 80 |
| step-by-step-guide | 80 |
| learning-ladder | 80 |
| playbook | 80 |
| flashcards | 80 |
| cheat-sheet | 90–100 |
| comparison-table | 90–100 |
| flowchart | 100 |
| timeline | 100 |
| mind-map | 100 |
| infographic | 100 |
| decision-tree | 100 |
| content-map | 100 |
| concept-stack | 100 |
| comic | 100 |
| architecture-diagram | 110–120 |
| sequence-diagram | 110–120 |
| dashboard | 120 |

## Hard rules

- **Never exceed the format's max width.** This is non-negotiable.
- **Prefer shrinking content over wrapping awkwardly.** A wrapped cell is worse than a shorter label.
- **Maintain alignment over verbosity.** If a column drifts to make text fit, drop characters from the text instead.

## Overflow handling (priority order)

If the planned content exceeds the format's max width:

1. **Shorten text.** Truncate labels, use abbreviations, drop articles ("the", "a").
2. **Restructure.** Break wide rows into stacked rows. Move labels outside boxes.
3. **Split into more panels.** Two narrow panels beat one wide panel that exceeds the budget.
4. **Never** widen past the max. Never.

## Width counting

- Count **printed columns**, not raw character bytes.
- Unicode box-drawing chars are single-column (1 col wide each).
- Some emoji are double-column — avoid emoji inside framed cells.
- Tabs are forbidden (rendering width varies by terminal). Use spaces.

## Per-line check

When QA runs (per `qa-checklist.md`), verify each line in the artifact:
```
max(len(line) for line in artifact) <= format_max_width
```
