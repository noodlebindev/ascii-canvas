# dashboard — full example

**Topic:** SponsorCal weekly metrics (bookings, MRR, churn, active creators, top creator, top sponsor)
**Width budget:** 120 cols
**Mode:** Unicode (default)

---

```
╔══════════════════════════════════════════════════════════════════════════════════════════════════════════════════════╗
║  SPONSORCAL WEEKLY METRICS                                                                    as of 2026-05-17       ║
╚══════════════════════════════════════════════════════════════════════════════════════════════════════════════════════╝
┌──────────────────────────────────────┬──────────────────────────────────────┬──────────────────────────────────────┐
│ Bookings (week)                      │ MRR                                  │ Churn                                │
│                       47  ▲          │                    $4,820  ▲          │                      2.1%  ▼         │
│  +12% vs last week                   │  +8% MoM ($370 added)                │  down from 3.4% last month           │
├──────────────────────────────────────┼──────────────────────────────────────┼──────────────────────────────────────┤
│ Active Creators                      │ Top Creator                          │ Top Sponsor                          │
│                      312  ▲          │               @sarah_writes  ▬        │                    Notion  ▬         │
│  +19 new this week                   │  $840 in bookings this week           │  3 slots booked this week            │
└──────────────────────────────────────┴──────────────────────────────────────┴──────────────────────────────────────┘
  Summary: Bookings and MRR both up; churn falling — best combined week since Stripe Connect launch.
```

---

## Why this works

- The 2×3 grid puts growth metrics (Bookings, MRR, Churn) in the top row and context metrics (Creators, Top Creator, Top Sponsor) in the bottom row, so a reader scanning top-to-bottom gets the business health signal first and the who-drove-it context second.
- Trend indicators (▲ ▼ ▬) are right-aligned on the value line, keeping all three metric blocks structurally identical — strict QA passes on cross-panel consistency.
- The summary line is outside all borders, matching the canonical skeleton, and gives a one-sentence synthesis that makes the dashboard complete without requiring the reader to synthesise across panels.
