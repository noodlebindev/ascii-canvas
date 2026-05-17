# infographic

## Purpose

Compress a topic into a single visual artifact with a headline, supporting blocks, and synthesis.

## Use when

- "Turn this into an infographic" requests
- High-signal summary that needs to feel shareable
- Data or insight distillation into a social-style asset
- One-pager that communicates the full picture at a glance

## Do NOT use when

- Narrative explanation is needed — use `slideshow`
- Reference lookup is needed — use `cheat-sheet`

## Width budget

100 cols

## Arc

A4 — Infographic arc (4–6 blocks): headline → 3 supporting insights → synthesis → optional CTA

## Layout rules

- Headline at top in heavy `╔═╗` border spanning full width
- 3 supporting blocks in a horizontal row — equal-width columns
- Each block: mini-icon (◆ / ▲ / ●) + BIG STAT / key phrase + label line
- Synthesis block at bottom in full-width single border
- Optional CTA in a centered footer line (`→ CTA text`)

## Canonical skeleton — Unicode

```
╔══════════════════════════════════════════════════════════════════════════════════════════════════╗
║                                      HEADLINE TEXT                                               ║
╚══════════════════════════════════════════════════════════════════════════════════════════════════╝
┌────────────────────────────────┬────────────────────────────────┬────────────────────────────────┐
│                                │                                │                                │
│       ◆  BIG STAT A            │       ▲  BIG STAT B            │       ●  BIG STAT C            │
│       Label for stat A         │       Label for stat B         │       Label for stat C         │
│                                │                                │                                │
└────────────────────────────────┴────────────────────────────────┴────────────────────────────────┘
┌──────────────────────────────────────────────────────────────────────────────────────────────────┐
│  Synthesis: <one to two sentence takeaway>                                                       │
└──────────────────────────────────────────────────────────────────────────────────────────────────┘
                               → CTA text / source / link
```

## Canonical skeleton — ASCII fallback

```
+================================================================================================+
|                                      HEADLINE TEXT                                             |
+================================================================================================+
+--------------------------------+--------------------------------+--------------------------------+
|                                |                                |                                |
|       *  BIG STAT A            |       ^  BIG STAT B            |       o  BIG STAT C            |
|       Label for stat A         |       Label for stat B         |       Label for stat C         |
|                                |                                |                                |
+--------------------------------+--------------------------------+--------------------------------+
+------------------------------------------------------------------------------------------------+
|  Synthesis: <one to two sentence takeaway>                                                     |
+------------------------------------------------------------------------------------------------+
                               -> CTA text / source / link
```

## Short rendered example

```
╔══════════════════════════════════════════════════════════════════════════════════════════════════╗
║                       WHY ASCII BEATS SCREENSHOTS IN DOCS                                        ║
╚══════════════════════════════════════════════════════════════════════════════════════════════════╝
┌────────────────────────────────┬────────────────────────────────┬────────────────────────────────┐
│                                │                                │                                │
│     ◆  PORTABLE                │     ▲  SEARCHABLE              │     ●  EDITABLE               │
│     Renders in any terminal,   │     Every word is indexed by   │     Change a label in 5 secs, │
│     editor, or chat window     │     grep, git log, and LLMs    │     no image editor needed    │
│                                │                                │                                │
└────────────────────────────────┴────────────────────────────────┴────────────────────────────────┘
┌──────────────────────────────────────────────────────────────────────────────────────────────────┐
│  Synthesis: ASCII diagrams have zero dependencies — they live alongside code, travel in PRs,     │
│  and degrade gracefully to plain text when Unicode isn't available.                              │
└──────────────────────────────────────────────────────────────────────────────────────────────────┘
                          → Try it: ask Claude for an ASCII diagram
```

## Failure modes

- If supporting blocks exceed 4 → split into 2 rows of blocks, keeping full-width headline and synthesis
- If headline + stats + synthesis don't tell a complete story → fall back to `slideshow`
- If width overflows 100 cols → shorten stat labels or reduce icon padding
