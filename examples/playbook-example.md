# playbook — full example

**Topic:** Cold outbound playbook — 6-step execution + 4 failure modes
**Width budget:** 80 cols
**Mode:** Unicode (default)

---

```
## Objective

Book 10 qualified sales demos per week through cold email outbound
to ICP targets, maintaining < 0.1% spam rate throughout.

---

## When to use

- ICP is fully defined and signed off by a decision-maker
- A verified lead list of 150–300 contacts is available
- Sending domain has been warmed for at least 3 weeks
- No active outbound campaign is running on the same domain

---

## Prerequisites

- ICP definition doc (industry, company size, title, pain signal)
- 200-lead list with verified direct emails (< 5% expected bounce)
- Sending domain warmed: age > 3 weeks, spam rate < 0.1%
- 3-touch sequence drafted: Touch 1 / Follow-up / Breakup email
- CRM or Instantly workspace ready to receive imported contacts

---

## Execution

### Step 1 — Verify and enrich the lead list

Action:  Run list through NeverBounce; remove Catch-All and Invalid.
Outcome: Clean list of 180–195 deliverable contacts.
Check:   NeverBounce report shows ≥ 92% "Valid" status.

### Step 2 — Import into sending tool

Action:  Upload cleaned CSV to Instantly; map Name, Email, Company.
Outcome: All contacts visible in campaign, status "Active".
Check:   Instantly shows correct count; no duplicate entries.

### Step 3 — Configure sending limits

Action:  Set daily cap to 40 emails/day; gap 90–180 sec between sends.
Outcome: Domain stays within safe warm-up thresholds.
Check:   Sending schedule shows ≤ 40/day for first two weeks.

### Step 4 — Launch and monitor deliverability

Action:  Start campaign; check Google Postmaster after 24 h.
Outcome: Domain reputation shows "Good" or "High".
Check:   Spam rate in Postmaster < 0.1%; bounce rate < 3%.

### Step 5 — Triage replies twice daily

Action:  Check Instantly inbox at 9 AM and 3 PM; tag each reply.
Outcome: Positive replies sent booking link within 4 hours.
Check:   No positive reply sits unread longer than 4 hours.

### Step 6 — Convert positives to demos

Action:  Send Calendly link; confirm meeting 24 h before via email.
Outcome: Demo calendar fills to target of 10/week.
Check:   Calendly shows ≥ 10 confirmed demos in 7-day window.

---

## Success criteria

✓ ≥ 10 demos booked within the 7-day send window
✓ Reply rate ≥ 3% across the full 3-touch sequence
✓ Spam complaint rate < 0.1% in Google Postmaster

---

## Failure modes

┌────────────────────────────────────┬───────────────────────────────────┐
│ Symptom                            │ Fix                               │
├────────────────────────────────────┼───────────────────────────────────┤
│ Open rate < 30% after 3 days       │ A/B test subject line; check      │
│                                    │ "From" name — use first name only │
├────────────────────────────────────┼───────────────────────────────────┤
│ Replies but no demo bookings       │ Shorten CTA; offer a specific     │
│                                    │ time slot instead of Calendly     │
├────────────────────────────────────┼───────────────────────────────────┤
│ Spam rate creeping above 0.05%     │ Pause campaign; audit list for    │
│                                    │ role-based emails and remove them │
├────────────────────────────────────┼───────────────────────────────────┤
│ Demos booked but high no-show rate │ Add 24 h + 1 h reminder emails;  │
│                                    │ ask for explicit "yes" reply      │
└────────────────────────────────────┴───────────────────────────────────┘
```

---

## Why this works

- Six steps cover the full execution arc (list → import → limits → launch → triage → convert) with distinct Action/Outcome/Check triplets so a new team member can hand-run the playbook without tribal knowledge.
- The failure-modes table uses multi-line cells (two lines per row) to fit detailed Fix text within the 37-col right column rather than truncating or overflowing the 80-col budget.
- Three measurable success criteria (count, rate, Postmaster metric) give an unambiguous pass/fail gate that avoids the "kinda worked" judgment call.
