# Box-drawing rules

The skill renders in **two modes**: Unicode (default) and pure ASCII (fallback). Both must produce layout-equivalent output.

## Character inventory

### Unicode (default)

| Class | Characters |
|---|---|
| Light box | `┌` `┐` `└` `┘` `─` `│` `├` `┤` `┬` `┴` `┼` |
| Heavy box | `┏` `┓` `┗` `┛` `━` `┃` `┣` `┫` `┳` `┻` `╋` |
| Double box | `╔` `╗` `╚` `╝` `═` `║` `╠` `╣` `╦` `╩` `╬` |
| Shapes | `◆` `▲` `●` `◇` `◯` `▼` `■` `□` `◉` `◎` |
| Arrows | `→` `←` `↑` `↓` `↔` `↕` `⇒` `⇐` `⇑` `⇓` |
| Misc | `•` `·` `◦` `※` `…` |

### ASCII fallback

| Purpose | Unicode | ASCII |
|---|---|---|
| Horizontal line | `─` | `-` |
| Vertical line | `│` | `\|` |
| Corner | `┌┐└┘` | `+` |
| T-junction | `├┤┬┴┼` | `+` |
| Arrow right | `→` | `->` |
| Arrow left | `←` | `<-` |
| Arrow down | `↓` | `v` |
| Arrow up | `↑` | `^` |
| Bullet | `•` | `*` |
| Diamond | `◆` | `<>` or `*` |

## Rules

### R1 — When to use ASCII fallback

Use pure ASCII when the user says:
- "plain ASCII"
- "email-safe"
- "copy-paste safe"
- "no special characters"

Also use pure ASCII when the destination is:
- Plain-text email body
- Code comments inside source files
- Logs / stdout in CI contexts
- Old terminals or constrained environments

In all other cases: Unicode default.

### R2 — Equivalence rule

The same layout MUST render in both modes without breaking alignment. When authoring a format file, provide BOTH a Unicode skeleton and an ASCII skeleton if they differ.

If a layout works in Unicode but breaks in ASCII (e.g. uses single-cell shapes that have no good ASCII equivalent), simplify the layout — don't break the equivalence.

### R3 — Consistency rule (line weights)

Do not mix Unicode line weights in a single artifact. Specifically:
- Don't mix `─` (light) with `═` (double) or `━` (heavy)
- Don't mix `│` (light) with `║` (double) or `┃` (heavy)

The only exception: when line weight carries semantic meaning (e.g. heavy outer frame to demarcate a "container" with light cells inside). Apply consistently — every outer frame uses the same weight.

### R4 — Arrow consistency

Within one artifact:
- All "forward" arrows use the same glyph (`→` everywhere, not `→` mixed with `>`)
- All "down" arrows use the same glyph (`↓` everywhere, not mixed with `v`)
- Arrow direction must match flow direction — never use `→` for a backward reference

### R5 — Closed boxes only

Every box must close. No dangling line segments. If a join would create an unclosed shape, restructure the layout.

### R6 — Bullet style consistency

Within one artifact, pick one bullet style and use it throughout:
- `•` (Unicode default)
- `*` (ASCII fallback)
- `-` (Markdown lists in saved files)

Do not mix.
