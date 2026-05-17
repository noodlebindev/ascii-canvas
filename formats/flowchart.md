# flowchart

## Purpose

Visualize a mixed process that contains both sequential steps and branching decisions.

## Use when

- A process has more than one decision point with alternate paths
- Representing code or system logic that includes conditionals
- Documenting a workflow where branches eventually merge back to a common path
- Showing loop-backs or retry logic

## Do NOT use when

- Pure yes/no branching to outcomes with no shared sequence — use `decision-tree`
- Pure linear sequence with no decisions — use `step-by-step-guide`
- Pure system topology / component relationships — use `architecture-diagram`

## Width budget

100 cols

## Arc

N/A — single artifact

## Layout rules

- Top-to-bottom flow; primary (happy) path goes straight down the center
- Decisions rendered as diamonds: `◆` markers with labels on the left and right sides (Unicode), `<>` blocks (ASCII)
- Branch labels (`Yes` / `No` / condition string) placed on the arrow leaving each decision point
- Process steps in labeled rectangular boxes using box-drawing characters
- Loop-backs drawn as a vertical line on the right margin with an upward-pointing arrow returning to the loop entry point
- Arrows between nodes use `│` (down), `▼` (into next box), `─►` (horizontal into branch)

## Canonical skeleton — Unicode

```
┌─────────────────────────────┐
│           START             │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│           Step 1            │
└──────────────┬──────────────┘
               │
               ▼
          ◆─────────◆
         ╱  Decision  ╲
        ◆               ◆
       ╱                 ╲
   Yes ▼                  ▼ No
┌──────────┐         ┌──────────┐
│  Path A  │         │  Path B  │
└─────┬────┘         └─────┬────┘
      │                    │
      └──────────┬──────────┘
                 │
                 ▼
┌─────────────────────────────┐
│             END             │
└─────────────────────────────┘
```

## Canonical skeleton — ASCII fallback

```
+-----------------------------+
|            START            |
+-------------+---------------+
              |
              v
+-----------------------------+
|            Step 1           |
+-------------+---------------+
              |
              v
           <Decision>
           /         \
        Yes             No
         v               v
+----------+         +----------+
|  Path A  |         |  Path B  |
+-----+----+         +-----+----+
      |                    |
      +----------+---------+
                 |
                 v
+-----------------------------+
|             END             |
+-----------------------------+
```

## Short rendered example

```
User Signup Flow
────────────────

┌─────────────────────────────┐
│            START            │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│         Submit form         │
└──────────────┬──────────────┘
               │
               ▼
          ◆─────────◆
         ╱   Valid?   ╲
        ◆               ◆
       ╱                 ╲
   Yes ▼                  ▼ No
┌──────────────┐     ┌─────────────────┐
│ Create acct  │     │  Show errors    │
└──────┬───────┘     └────────┬────────┘
       │                      │
       ▼                      │ (loop back)
┌──────────────┐              │
│ Send welcome │              │
│   email      │              │
└──────┬───────┘              │
       │              ┌───────┘
       │              │
       │       ┌──────▼──────────────────┐
       │       │      Submit form        │  ◄── loop
       │       └─────────────────────────┘
       │
       ▼
┌─────────────────────────────┐
│             END             │
└─────────────────────────────┘
```

## Failure modes

- If decisions exceed 3 in a single flow → split into linked sub-flowcharts, each within width budget
- If width overflows at 100 cols → shorten step labels; if still failing, fall back to `step-by-step-guide`
- If flow has no shared sequence — only pure branching to separate outcomes → switch to `decision-tree`
- If loop-backs make the diagram unreadable → extract the loop as a named sub-process and reference it from the main flow
