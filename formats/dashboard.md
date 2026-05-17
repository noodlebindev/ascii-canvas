# dashboard

## Purpose

Status board showing key metrics and sections at a glance.

## Use when

- Weekly status summaries or KPI snapshots
- Ops boards for a product, campaign, or project
- "Give me a dashboard for X" requests
- Multi-metric summaries where comparison across panels matters

## Do NOT use when

- Narrative explanation is needed — use `slideshow`
- Single-purpose reference card — use `cheat-sheet`

## Width budget

120 cols

## Arc

A7 — Dashboard arc (4–8 panels): title → metrics → summary

## Layout rules

- Top banner: title + as-of date in heavy border spanning full width
- 2×3 or 3×2 grid of metric blocks — equal column widths
- Each block: metric name, BIG value, trend indicator (▲ ▼ ▬), one supporting line
- Bottom: one-line summary in a full-width footer
- Total width ≤ 120 cols; each metric block ≤ 36 cols inner width in a 3-col grid

## Canonical skeleton — Unicode

```
╔══════════════════════════════════════════════════════════════════════════════════════════════════════╗
║  DASHBOARD TITLE                                                              as of <Date>           ║
╚══════════════════════════════════════════════════════════════════════════════════════════════════════╝
┌──────────────────────────────────┬──────────────────────────────────┬──────────────────────────────────┐
│ <Metric A>                       │ <Metric B>                       │ <Metric C>                       │
│         BIG VALUE  ▲             │         BIG VALUE  ▼             │         BIG VALUE  ▬             │
│  Supporting detail               │  Supporting detail               │  Supporting detail               │
├──────────────────────────────────┼──────────────────────────────────┼──────────────────────────────────┤
│ <Metric D>                       │ <Metric E>                       │ <Metric F>                       │
│         BIG VALUE  ▲             │         BIG VALUE  ▼             │         BIG VALUE  ▬             │
│  Supporting detail               │  Supporting detail               │  Supporting detail               │
└──────────────────────────────────┴──────────────────────────────────┴──────────────────────────────────┘
  Summary: <one-line insight or status note>
```

## Canonical skeleton — ASCII fallback

```
+=====================================================================================================+
|  DASHBOARD TITLE                                                              as of <Date>          |
+=====================================================================================================+
+----------------------------------+----------------------------------+----------------------------------+
| <Metric A>                       | <Metric B>                       | <Metric C>                       |
|         BIG VALUE  ^             |         BIG VALUE  v             |         BIG VALUE  -             |
|  Supporting detail               |  Supporting detail               |  Supporting detail               |
+----------------------------------+----------------------------------+----------------------------------+
| <Metric D>                       | <Metric E>                       | <Metric F>                       |
|         BIG VALUE  ^             |         BIG VALUE  v             |         BIG VALUE  -             |
|  Supporting detail               |  Supporting detail               |  Supporting detail               |
+----------------------------------+----------------------------------+----------------------------------+
  Summary: <one-line insight or status note>
```

## Short rendered example

```
╔══════════════════════════════════════════════════════════════════════════════════════════════════════╗
║  SPONSORCAL WEEKLY METRICS                                                    as of 2026-05-17       ║
╚══════════════════════════════════════════════════════════════════════════════════════════════════════╝
┌──────────────────────────────────┬──────────────────────────────────┬──────────────────────────────────┐
│ Bookings (week)                  │ MRR                              │ Churn                            │
│              14  ▲               │          $4,210  ▲               │            1.8%  ▼               │
│  +3 vs last week                 │  +$310 vs last month             │  -0.3 pp vs last month           │
├──────────────────────────────────┼──────────────────────────────────┼──────────────────────────────────┤
│ Active Creators                  │ Top Creator                      │ Top Sponsor                      │
│              87  ▲               │       morningbrew  ▬             │         adswipe.io  ▬            │
│  +5 new this week                │  $1,200 booked                   │  3 slots bought                  │
└──────────────────────────────────┴──────────────────────────────────┴──────────────────────────────────┘
  Summary: Strong week — bookings up, churn falling, MRR on track for $5k by month-end.
```

## Failure modes

- If metrics exceed 8 → split into themed dashboards (Growth / Ops / Finance)
- If supporting lines need detail → fall back to `cheat-sheet` with multi-section layout
- If width overflows 120 cols → reduce to 2-col grid (2×3) or shorten metric labels
