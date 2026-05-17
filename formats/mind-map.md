# mind-map

## Purpose

Central idea with radial branches of related concepts.

## Use when

- Brainstorming — exploring all facets of a topic
- Ideation around a core concept before writing or building
- Mapping related ideas that don't have a strict hierarchy

## Do NOT use when

- Content packaging across multiple formats — use `content-map`
- Strict dependency hierarchy — use `concept-stack`

## Width budget

100 cols

## Arc

N/A — single artifact

## Layout rules

- Central `[Core Idea]` box at top (or left-center for wide layouts)
- Branches spread below with `┬` / `├` / `└` connectors
- Depth ≤ 3: root → branch → leaf
- Each leaf is one concept, formatted as `• <concept>`
- No crossing lines

## Canonical skeleton — Unicode

```
                      ┌─────────────┐
                      │  Core Idea  │
                      └──────┬──────┘
           ┌──────────────────┼──────────────────┐
           ▼                  ▼                  ▼
    ┌──────────┐       ┌──────────┐       ┌──────────┐
    │ Branch A │       │ Branch B │       │ Branch C │
    └────┬─────┘       └────┬─────┘       └────┬─────┘
         │                  │                  │
    • Leaf A1          • Leaf B1          • Leaf C1
    • Leaf A2          • Leaf B2          • Leaf C2
    • Leaf A3          • Leaf B3          • Leaf C3
```

## Canonical skeleton — ASCII fallback

```
                      +-------------+
                      |  Core Idea  |
                      +------+------+
           +------------------+------------------+
           v                  v                  v
    +----------+       +----------+       +----------+
    | Branch A |       | Branch B |       | Branch C |
    +----+-----+       +----+-----+       +----+-----+
         |                  |                  |
    * Leaf A1          * Leaf B1          * Leaf C1
    * Leaf A2          * Leaf B2          * Leaf C2
    * Leaf A3          * Leaf B3          * Leaf C3
```

## Short rendered example

```
                   ┌───────────────────┐
                   │  ASCII Diagrams   │
                   └────────┬──────────┘
          ┌─────────────────┼─────────────────┐
          ▼                 ▼                 ▼
   ┌─────────────┐  ┌─────────────┐  ┌─────────────┐
   │   Formats   │  │  Use Cases  │  │    Tools    │
   └──────┬──────┘  └──────┬──────┘  └──────┬──────┘
          │                │                │
   • flowchart      • documentation  • Claude Code
   • timeline       • onboarding     • Copilot
   • cheat-sheet    • PRs/reviews    • terminal
```

## Failure modes

- If depth exceeds 3 → switch to `concept-stack` or `content-map`
- If layout is too wide → reorient to vertical (branch list with indented sub-bullets)
- If branches need ordering or dependencies → switch to `concept-stack`
