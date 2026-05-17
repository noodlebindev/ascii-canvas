# mind-map — full example

**Topic:** ASCII diagrams — formats, use cases, tools, taxonomy
**Width budget:** 100 cols
**Mode:** Unicode (default)

---

```
                              ┌───────────────────┐
                              │   ASCII diagrams  │
                              └─────────┬─────────┘
              ┌───────────────────────────┬───────────────────────────┐
              ▼                           ▼                           ▼
      ┌──────────────┐          ┌──────────────────┐          ┌──────────────┐
      │   Formats    │          │   Use cases      │          │    Tools     │
      └──────┬───────┘          └────────┬─────────┘          └──────┬───────┘
             │                           │                            │
      • flowchart               • technical docs              • graph-easy
      • slideshow               • PR reviews                  • asciiflow
      • cheat-sheet             • teaching / talks            • ditaa
      • sequence diagram        • LLM context                 • Claude Code
      • mind-map                                              • monodraw
             │
      ┌──────────────┐
      │   Taxonomy   │
      └──────┬───────┘
             │
      • by encoding   (Unicode vs ASCII)
      • by scope      (single artifact vs multi-panel)
      • by concept    (process / structure / data / narrative)
      • by direction  (top-down / left-right / radial)
```

---

## Why this works

- Four branches (Formats, Use Cases, Tools, Taxonomy) give balanced coverage of the "ASCII diagrams" topic space — not too deep, not too shallow; each branch has 4–5 leaves that are genuinely distinct.
- Taxonomy is placed as a vertical sub-branch below Formats to avoid a four-way split that would overflow 100 cols; three main branches across the top keeps the widest row under 80 chars.
- Leaves use `•` bullets consistently throughout (no mixing with `-` or `*`), satisfying the cross-artifact bullet-style rule.

## ASCII variant (if structurally different from Unicode)

```
                              +-------------------+
                              |   ASCII diagrams  |
                              +--------+----------+
              +-------------------------+-------------------------+
              v                         v                         v
      +--------------+        +------------------+        +--------------+
      |   Formats    |        |   Use cases      |        |    Tools     |
      +------+-------+        +--------+---------+        +------+-------+
             |                         |                          |
      * flowchart               * technical docs          * graph-easy
      * slideshow               * PR reviews              * asciiflow
      * cheat-sheet             * teaching / talks        * ditaa
      * sequence diagram        * LLM context             * Claude Code
      * mind-map                                          * monodraw
             |
      +--------------+
      |   Taxonomy   |
      +------+-------+
             |
      * by encoding   (Unicode vs ASCII)
      * by scope      (single vs multi-panel)
      * by concept    (process / structure / data / narrative)
      * by direction  (top-down / left-right / radial)
```
