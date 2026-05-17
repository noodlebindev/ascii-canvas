# playbook

## Purpose

A repeatable workflow / SOP with clear objective, prerequisites, sequenced steps, success criteria, and failure modes.

## Use when

- Documenting a process you will run more than once (SOP / runbook)
- Specifying an AI agent system or automated workflow
- Marketing or ops execution plans that need to be handed off or repeated
- Any situation where "what does success look like?" must be defined up front

## Do NOT use when

- Simple linear walkthrough without prerequisites or success criteria — use `step-by-step-guide`
- Teaching a concept — use `slideshow`
- Pure decision logic with no execution steps — use `decision-tree` or `flowchart`

## Width budget

80 cols

## Arc

A2 — Playbook arc (5–8 panels): objective → when to use → prerequisites → steps → success criteria → failure modes

## Layout rules

- Each arc section is a `## Section` heading
- Steps inside the "Execution" section get numbered (`### Step 1`, `### Step 2`, ...)
- Each step has exactly three labeled lines: `Action:`, `Outcome:`, `Check:`
- Success criteria block uses `✓` markers (Unicode) or `[x]` (ASCII fallback)
- Failure modes block is a 2-col table with `┌─┬─┐` borders (Unicode) or `+---+` (ASCII fallback)

## Canonical skeleton — Unicode

```
## Objective

<One sentence: what this playbook achieves when executed correctly.>

---

## When to use

- <Trigger condition>
- <Trigger condition>

---

## Prerequisites

- <Required input or resource>
- <Required input or resource>

---

## Execution

### Step 1 — <verb phrase>

Action:  <what to do>
Outcome: <what changes as a result>
Check:   <how to verify it worked>

### Step 2 — <verb phrase>

Action:  <what to do>
Outcome: <what changes as a result>
Check:   <how to verify it worked>

---

## Success criteria

✓ <measurable outcome>
✓ <measurable outcome>
✓ <measurable outcome>

---

## Failure modes

┌──────────────────────────────────────┬───────────────────────────────────────┐
│ Symptom                              │ Fix                                   │
├──────────────────────────────────────┼───────────────────────────────────────┤
│ <symptom description>                │ <corrective action>                   │
│ <symptom description>                │ <corrective action>                   │
└──────────────────────────────────────┴───────────────────────────────────────┘
```

## Canonical skeleton — ASCII fallback

```
## Objective

<One sentence: what this playbook achieves when executed correctly.>

---

## When to use

- <Trigger condition>
- <Trigger condition>

---

## Prerequisites

- <Required input or resource>
- <Required input or resource>

---

## Execution

### Step 1 -- <verb phrase>

Action:  <what to do>
Outcome: <what changes as a result>
Check:   <how to verify it worked>

### Step 2 -- <verb phrase>

Action:  <what to do>
Outcome: <what changes as a result>
Check:   <how to verify it worked>

---

## Success criteria

[x] <measurable outcome>
[x] <measurable outcome>
[x] <measurable outcome>

---

## Failure modes

+--------------------------------------+---------------------------------------+
| Symptom                              | Fix                                   |
+--------------------------------------+---------------------------------------+
| <symptom description>                | <corrective action>                   |
| <symptom description>                | <corrective action>                   |
+--------------------------------------+---------------------------------------+
```

## Short rendered example

Cold outbound playbook — book 10 demos per week:

```
## Objective

Run cold outbound email to book 10 qualified demos per week from ICP targets.

---

## When to use

- ICP is defined and a verified lead list is available
- Sending cadence is < 200 emails/day to avoid domain warm-up issues

---

## Prerequisites

- ICP definition doc signed off
- 200-lead verified list with direct emails
- Sending domain warmed (>3 weeks, <0.1% spam rate)
- Email sequence drafted (3 touches, 5-7 day gaps)

---

## Execution

### Step 1 -- Build lead list

Action:  Export ICP-matching leads from Apollo; verify emails via NeverBounce.
Outcome: 200 verified contacts, <5% bounce rate expected.
Check:   NeverBounce report shows >= 95% "valid" status.

### Step 2 -- Load sequence

Action:  Import list into Instantly; assign to 3-touch sequence.
Outcome: All contacts enqueued for send starting Day 1.
Check:   Instantly dashboard shows 200 contacts "active."

### Step 3 -- Monitor and reply-triage

Action:  Check replies 2x/day; move positives to demo booking link.
Outcome: Warm replies converted to calendar invites within 4h.
Check:   >= 10 demos booked by Day 7.

---

## Success criteria

[x] >= 10 demos booked in the 7-day window
[x] Reply rate >= 3% across the sequence
[x] Spam complaints < 0.1% of sends

---

## Failure modes

+--------------------------------------+---------------------------------------+
| Symptom                              | Fix                                   |
+--------------------------------------+---------------------------------------+
| Low open rate on outreach            | Improve subject line and from name    |
| No replies after 3 touches           | Shorten email; add social proof       |
| Demos booked but no shows            | Send reminder 24h and 1h before       |
+--------------------------------------+---------------------------------------+
```

## Failure modes

- If steps < 3 → fall back to `step-by-step-guide` (playbook overhead is unwarranted)
- If width overflows → shorten Action/Outcome/Check phrasing; if still tight, split failure-modes table to its own section
- If prerequisites are trivial → collapse into a single bullet and merge with the Objective section
