# cheat-sheet

## Purpose

Dense reference card — maximal information density per square inch, for lookup not learning.

## Use when

- Quick reference while working (commands, keyboard shortcuts, syntax)
- A user asks "give me a cheat sheet for X"
- Content is a list of term-definition pairs that must be scannable at a glance
- Reference card that will be re-visited, not read once

## Do NOT use when

- Narrative explanation is needed — use `slideshow`
- Side-by-side options that need evaluation to choose between — use `comparison-table`

## Width budget

90–100 cols (target 95)

## Arc

N/A — single artifact (optionally multi-section within one frame)

## Layout rules

- Title in heavy `╔═╗` border spanning full width
- Multi-column layout when content fits — 2 equal columns of 44-char inner content each
- Section headers embedded in top or mid borders using `┌─ Section Name ─┬─ Section Name ─┐`
- One concept per line: `<term>  · <definition>` style with `·` separator (Unicode) or `:` (ASCII)
- No wasted vertical space — entries are tightly packed with one blank row between sections
- Single-column fallback if content is sparse or definitions are long

## Canonical skeleton — Unicode

```
╔═════════════════════════════════════════════════════════════════════════════════════════════╗
║                                            TITLE                                            ║
╚═════════════════════════════════════════════════════════════════════════════════════════════╝
┌─ <Section A> ────────────────────────────────┬─ <Section B> ────────────────────────────────┐
│                                              │                                              │
│ <term>  · <definition>                       │ <term>  · <definition>                       │
│ <term>  · <definition>                       │ <term>  · <definition>                       │
│                                              │                                              │
├─ <Section C> ────────────────────────────────┼─ <Section D> ────────────────────────────────┤
│                                              │                                              │
│ <term>  · <definition>                       │ <term>  · <definition>                       │
│ <term>  · <definition>                       │ <term>  · <definition>                       │
│                                              │                                              │
└──────────────────────────────────────────────┴──────────────────────────────────────────────┘
```

## Canonical skeleton — ASCII fallback

```
+=============================================================================================+
|                                            TITLE                                            |
+=============================================================================================+
+- <Section A> --------------------------------+- <Section B> --------------------------------+
|                                              |                                              |
| <term> : <definition>                        | <term> : <definition>                        |
| <term> : <definition>                        | <term> : <definition>                        |
|                                              |                                              |
+- <Section C> --------------------------------+- <Section D> --------------------------------+
|                                              |                                              |
| <term> : <definition>                        | <term> : <definition>                        |
| <term> : <definition>                        | <term> : <definition>                        |
|                                              |                                              |
+----------------------------------------------+----------------------------------------------+
```

## Short rendered example

Git cheat sheet with 2 sections (Stage/Commit and Branch):

```
╔═════════════════════════════════════════════════════════════════════════════════════════════╗
║                                       GIT CHEAT SHEET                                       ║
╚═════════════════════════════════════════════════════════════════════════════════════════════╝
┌─ Stage / Commit ─────────────────────────────┬─ Branch ─────────────────────────────────────┐
│                                              │                                              │
│ git add <file>   · stage a file              │ git branch       · list branches             │
│ git add .        · stage all changes         │ git branch <n>   · create branch             │
│ git commit -m    · commit staged             │ git checkout <b> · switch branch             │
│ git commit --amend · amend last commit       │ git branch -d <b>· delete branch             │
│                                              │                                              │
└──────────────────────────────────────────────┴──────────────────────────────────────────────┘
```

## Failure modes

- If content is sparse (< 4 entries per section) → switch to single-column layout
- If a definition is too long for 44-char inner column → abbreviate the term or split into 2 rows
- If sections grow past 10 entries each → split into multi-panel cheat-sheet, one panel per topic cluster
- If entries need ordering or dependency context → switch to `step-by-step-guide` or `playbook`
