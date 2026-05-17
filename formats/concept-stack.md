# concept-stack

## Purpose

Show layers or dependencies where each layer rests on the one below.

## Use when

- "Show me how X builds on Y" — abstraction layers
- Tech stack visualization
- Systems-thinking layouts with clear foundation-to-outcome flow
- Concepts that can't be understood without the layer beneath

## Do NOT use when

- System topology with cross-connections between layers — use `architecture-diagram`
- Ideas radiating outward from a center — use `mind-map`

## Width budget

100 cols

## Arc

A5 — Concept-stack arc (4–6 layers): base → supporting layers → top outcome

## Layout rules

- Layers stacked vertically — top outcome at top, foundation at bottom
- Uniform width OR pyramid-widening (widest at bottom) — both valid
- Each layer: name + 1-line role description
- Implicit "depends on" semantics — no connection labels needed between layers
- `▲` between layers optional (use for clarity in tall stacks)

## Canonical skeleton — Unicode

```
┌──────────────────────────────────────────────────────────────┐
│  Layer 5 — Outcome          role: <top outcome>              │
├──────────────────────────────────────────────────────────────┤
│  Layer 4 — <name>           role: <function>                 │
├──────────────────────────────────────────────────────────────┤
│  Layer 3 — <name>           role: <function>                 │
├──────────────────────────────────────────────────────────────┤
│  Layer 2 — <name>           role: <function>                 │
├──────────────────────────────────────────────────────────────┤
│  Layer 1 — Foundation       role: <base layer>               │
└──────────────────────────────────────────────────────────────┘
```

## Canonical skeleton — ASCII fallback

```
+--------------------------------------------------------------+
|  Layer 5 -- Outcome          role: <top outcome>             |
+--------------------------------------------------------------+
|  Layer 4 -- <name>           role: <function>                |
+--------------------------------------------------------------+
|  Layer 3 -- <name>           role: <function>                |
+--------------------------------------------------------------+
|  Layer 2 -- <name>           role: <function>                |
+--------------------------------------------------------------+
|  Layer 1 -- Foundation       role: <base layer>              |
+--------------------------------------------------------------+
```

## Short rendered example

```
Modern Web App Stack
────────────────────

┌──────────────────────────────────────────────────────────────┐
│  CDN / Edge        — serves static assets, caches responses  │
├──────────────────────────────────────────────────────────────┤
│  SSR Framework     — renders pages, handles routing          │
├──────────────────────────────────────────────────────────────┤
│  REST / GraphQL API — exposes business logic to the client   │
├──────────────────────────────────────────────────────────────┤
│  ORM               — maps objects to relational tables       │
├──────────────────────────────────────────────────────────────┤
│  Database          — persists all application state          │
└──────────────────────────────────────────────────────────────┘
```

## Failure modes

- If layers exceed 6 → group adjacent layers into named tiers, then stack the tiers
- If lateral connections are needed between layers → switch to `architecture-diagram`
- If layers are not dependencies (no "builds on" relationship) → switch to `mind-map`
