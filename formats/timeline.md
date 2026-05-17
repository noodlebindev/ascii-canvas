# timeline

## Purpose

Show events sequenced on a horizontal or vertical axis.

## Use when

- History of a project, product, or concept
- Product roadmap or project schedule
- Sequence of past events in chronological order
- Milestones where date context matters

## Do NOT use when

- Events have decision branches — use `flowchart`
- Concept dependencies without time — use `concept-stack`

## Width budget

100 cols

## Arc

N/A — single artifact

## Layout rules

- Vertical timeline preferred for >4 events
- Horizontal timeline for ≤4 short labels
- Each event: date/label + title + 1-line description
- Anchor markers (`●`) on the axis at each event
- `│` connects anchor points in vertical layout; `─` in horizontal

## Canonical skeleton — Unicode

Vertical (preferred for >4 events):

```
           TIMELINE TITLE
           ──────────────

  <Date 1> ● <Event Title 1>
           │   <One-line description>
           │
  <Date 2> ● <Event Title 2>
           │   <One-line description>
           │
  <Date 3> ● <Event Title 3>
           │   <One-line description>
           │
  <Date 4> ● <Event Title 4>
               <One-line description>
```

Horizontal (for ≤4 short labels):

```
  ●──────────────●──────────────●──────────────●
<Label 1>    <Label 2>    <Label 3>    <Label 4>
<Title 1>    <Title 2>    <Title 3>    <Title 4>
```

## Canonical skeleton — ASCII fallback

Vertical:

```
           TIMELINE TITLE
           --------------

  <Date 1> * <Event Title 1>
           |   <One-line description>
           |
  <Date 2> * <Event Title 2>
           |   <One-line description>
           |
  <Date 3> * <Event Title 3>
           |   <One-line description>
           |
  <Date 4> * <Event Title 4>
               <One-line description>
```

Horizontal:

```
  *--------------*--------------*--------------*
<Label 1>    <Label 2>    <Label 3>    <Label 4>
<Title 1>    <Title 2>    <Title 3>    <Title 4>
```

## Short rendered example

```
        SPONSORCAL MILESTONES
        ─────────────────────

  Q1 2025 ● Idea & validation
           │   Identified creator monetisation gap
           │
  Q3 2025 ● Private beta
           │   First 10 newsletter creators onboarded
           │
  Q4 2025 ● Stripe Connect live
           │   End-to-end payments shipped
           │
  Q1 2026 ● Public launch
           │   Open signup, marketing site live
           │
  Q2 2026 ● Media kit feature
               Verified open-rate cards for creators
```

## Failure modes

- If events exceed 12 → split into era-based timelines with a shared legend
- If branching forks appear → switch to `flowchart`
- If width overflows at 100 cols → shorten descriptions or use vertical layout
