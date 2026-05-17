# learning-ladder

## Purpose

Show a skill or topic progressing from beginner to expert across discrete rungs.

## Use when

- "Make a learning path for X" requests
- Skill-progression maps from foundations to mastery
- Curriculum design or education content
- Structured skill-building that builds on prior levels

## Do NOT use when

- Linear how-to with no skill levels — use `step-by-step-guide`
- Concept dependency without skill progression — use `concept-stack`

## Width budget

80 cols

## Arc

A3 — Learning-ladder arc (4–6 levels): foundations → mechanics → application → intermediate → advanced → expert

## Layout rules

- Vertical ladder — rungs from bottom (foundations) to top (expert)
- Each rung: level name + 2-3 sub-skills as `•` bullets
- `▲` between rungs (centered) to show upward progression
- Rung boxes ≤ 76 cols wide
- Present from top (expert) to bottom (foundations) in the file — read top-down as aspirational

## Canonical skeleton — Unicode

```
┌──────────────────────────────────────────────┐
│  Level 6 — Expert                            │
│  • Sub-skill 1                               │
│  • Sub-skill 2                               │
└──────────────────────────────────────────────┘
                       ▲
┌──────────────────────────────────────────────┐
│  Level 5 — Advanced                          │
│  • Sub-skill 1                               │
│  • Sub-skill 2                               │
└──────────────────────────────────────────────┘
                       ▲
┌──────────────────────────────────────────────┐
│  Level 4 — Intermediate                      │
│  • Sub-skill 1                               │
│  • Sub-skill 2                               │
└──────────────────────────────────────────────┘
                       ▲
┌──────────────────────────────────────────────┐
│  Level 3 — Application                       │
│  • Sub-skill 1                               │
│  • Sub-skill 2                               │
└──────────────────────────────────────────────┘
                       ▲
┌──────────────────────────────────────────────┐
│  Level 2 — Mechanics                         │
│  • Sub-skill 1                               │
│  • Sub-skill 2                               │
└──────────────────────────────────────────────┘
                       ▲
┌──────────────────────────────────────────────┐
│  Level 1 — Foundations                       │
│  • Sub-skill 1                               │
│  • Sub-skill 2                               │
└──────────────────────────────────────────────┘
```

## Canonical skeleton — ASCII fallback

```
+----------------------------------------------+
|  Level 6 -- Expert                           |
|  * Sub-skill 1                               |
|  * Sub-skill 2                               |
+----------------------------------------------+
                       ^
+----------------------------------------------+
|  Level 5 -- Advanced                         |
|  * Sub-skill 1                               |
|  * Sub-skill 2                               |
+----------------------------------------------+
                       ^
+----------------------------------------------+
|  Level 4 -- Intermediate                     |
|  * Sub-skill 1                               |
|  * Sub-skill 2                               |
+----------------------------------------------+
                       ^
+----------------------------------------------+
|  Level 3 -- Application                      |
|  * Sub-skill 1                               |
|  * Sub-skill 2                               |
+----------------------------------------------+
                       ^
+----------------------------------------------+
|  Level 2 -- Mechanics                        |
|  * Sub-skill 1                               |
|  * Sub-skill 2                               |
+----------------------------------------------+
                       ^
+----------------------------------------------+
|  Level 1 -- Foundations                      |
|  * Sub-skill 1                               |
|  * Sub-skill 2                               |
+----------------------------------------------+
```

## Short rendered example

```
Spanish Verb Conjugation Ladder
────────────────────────────────

┌──────────────────────────────────────────────┐
│  Level 6 — Fluency                           │
│  • Sequence of tenses across clauses         │
│  • Vosotros / regional variants              │
└──────────────────────────────────────────────┘
                       ▲
┌──────────────────────────────────────────────┐
│  Level 5 — Advanced Uses                     │
│  • Conditional perfect (habría hecho)        │
│  • Passive voice with ser + participle       │
└──────────────────────────────────────────────┘
                       ▲
┌──────────────────────────────────────────────┐
│  Level 4 — Subjunctive                       │
│  • Present subjunctive (quiero que vengas)   │
│  • Imperfect subjunctive (si tuviera...)     │
└──────────────────────────────────────────────┘
                       ▲
┌──────────────────────────────────────────────┐
│  Level 3 — Preterite & Imperfect             │
│  • Preterite: completed past actions         │
│  • Imperfect: ongoing/habitual past          │
└──────────────────────────────────────────────┘
                       ▲
┌──────────────────────────────────────────────┐
│  Level 2 — Common Irregulars                 │
│  • Stem-changers (e→ie, o→ue)                │
│  • Ser / estar / ir / tener / haber          │
└──────────────────────────────────────────────┘
                       ▲
┌──────────────────────────────────────────────┐
│  Level 1 — Present Tense                     │
│  • Regular -ar / -er / -ir endings           │
│  • Reflexive verbs (levantarse)              │
└──────────────────────────────────────────────┘
```

## Failure modes

- If levels are fewer than 4 → fall back to `step-by-step-guide`
- If levels are not progressive (no dependency between rungs) → switch to `concept-stack` or `mind-map`
- If width overflows 80 cols → shorten sub-skill labels; do not widen boxes
