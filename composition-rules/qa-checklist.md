# QA checklist

Two modes: **light** (single in-chat diagrams) and **strict** (saved/multi-panel/reusable/publishable artifacts).

## Light QA

Quick visual sanity check. Look at the rendered output and confirm:
- Alignment looks right
- Width fits the format budget
- Boxes appear closed

That's it. Don't over-engineer.

## Strict QA — 8-point checklist

Run before BOTH chat render AND file write. Do not write a file that has not passed strict QA.

1. **Every box closes.** No dangling line segments. No unclosed `┌─┐` without a matching `└─┘`.
2. **Every column aligns.** Vertical lines (`│`) line up across rows. Cell widths match within a column.
3. **No line exceeds the format width budget.** Verify `max(len(line)) <= format_max_width`.
4. **No awkward mid-cell wrapping.** Text inside a cell does not break across rendered lines.
5. **Arrows/connectors are readable.** Directions match flow. No ambiguous joins (where two arrows could be read as one).
6. **Unicode and ASCII fallback structures stay layout-equivalent.** If the user requested ASCII, verify the ASCII version preserves the same row/column structure.
7. **Section spacing is consistent.** All major separators identical (`---` or `===`, not mixed). All minor spacings (blank lines between sections) match.
8. **Markdown code fences preserve formatting.** When wrapped in ` ``` ` blocks, no line is broken or auto-formatted by markdown.

## Cross-artifact consistency check (in addition to the 8 points)

Verify repeated structural elements stay consistent across the WHOLE artifact:
- All boxes use the same line weight (per box-drawing.md R3)
- All panels in a multi-panel artifact have **identical width**
- All section dividers identical (no `---` and `===` mixed)
- All bullet styles match (no `•` and `-` mixed)
- All arrows pointing the same direction use the same glyph

This catches drift that point-checks on individual sections miss.

## When QA runs

- **Light QA:** every single in-chat artifact.
- **Strict QA:** every saved artifact, every multi-panel artifact, anything explicitly tagged "publish" or "reusable".
- **Strict QA runs twice:**
  1. Before rendering to chat
  2. Before writing to file
- **Pre-write gate:** the file write step must not execute unless strict QA has passed. If QA fails between render and write, regenerate, do not save the failing version.

## Failure behavior

- **Silently fix issues.** Do not surface minor corrections to the user.
- **Only warn the user** if the requested layout cannot fit cleanly at the chosen width — e.g., "Note: this is tight at 80 cols. Want me to widen to 100?"

## Fail-twice → simplify rule

If layout fails strict QA twice in a row:
- Reduce text
- Split into more panels
- Switch to a narrower/simpler format (see fallback map below)
- Move labels outside boxes
- Never force dense text into tight boxes

## Format fallback map (graceful degradation)

When the simplify rule cannot save the layout, fall back to a simpler adjacent format:

| Original | Fallback |
|---|---|
| playbook | step-by-step-guide |
| slideshow | infographic |
| infographic | cheat-sheet |
| dashboard | cheat-sheet |
| architecture-diagram | concept-stack |
| sequence-diagram | step-by-step-guide |
| mind-map | content-map |
| concept-stack | comparison-table |
| learning-ladder | step-by-step-guide |
| content-map | infographic |
| flowchart | step-by-step-guide |
| decision-tree | comparison-table |

When fallback fires, emit a one-line note:
```
Note: simplified from <original> to <fallback> for readability.
```

## No partial save rule

NEVER save:
- A preview render (chat preview shows first 1–2 sections; the file write must contain the FULL artifact)
- An artifact that failed strict QA
- An in-progress retry during the fail-twice cycle
- An interrupted generation

The pre-write gate: full artifact assembled + strict QA passed → then and only then write.

## Readability override

If strict QA passes but the artifact is still hard to read (dense, overcrowded, visually noisy):
- Simplify anyway
- A pass on the checklist is necessary but not sufficient — readability is the real goal

## General layout principles (enforced as part of QA)

### L1 — Label placement

If text does not fit inside a box at the format's width budget:
- Place the label outside the box, with a leader line (e.g. `── label`)
- Never force-cram text past box boundaries
- Never wrap inside a cell

### L2 — Visual hierarchy

- Primary content goes top or left
- Indentation signals dependency / subordination
- Proximity (no gap) + shared border = relationship
- Negative space (a blank line) signals "this is a new group"

When the artifact's hierarchy doesn't match the topic's hierarchy → restructure.

### L3 — Density control

- Default to compact layouts. Minimize whitespace.
- Only increase spacing when readability genuinely requires it (e.g. dashboard metric blocks need breathing room; a cheat-sheet does not)
- If the artifact feels sparse → tighten before shipping
- If the artifact feels claustrophobic → simplify (drop content) before widening spacing
