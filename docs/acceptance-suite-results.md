# Acceptance suite — 2026-05-17

## Prompt 1: "Make me a flowchart of how user signup works in a typical web app."

**Expected:** routes to flowchart, no file save, single-artifact at ≤100 cols

**Observed:** Skill activated. Routed to `flowchart` format (explicit keyword "flowchart"
+ branching + mixed steps). Unicode default. Rendered inline with ≥2 decision diamonds
(◆), Yes/No branch labels, rectangular step boxes, and a loop-back for validation errors.
No file created.

**Structural checks:**
- (a) decision node present (◆): PASS
- (b) Yes/No labels on every branch: PASS
- (c) max line width ≤ 100: PASS (max 69 cols)
- (d) no `---` section dividers: PASS (single artifact, no `---` dividers)
- (e) NO file created in `~/Ascii-diagrams/`: PASS

**Verdict:** PASS

---

## Prompt 2: "Break down how Spanish verb conjugation works for a learner — visually."

**Expected:** routes to learning-ladder, 4–6 levels, each boxed, ▲ between rungs,
≤80 cols, file created at `~/Ascii-diagrams/2026-05/2026-05-17-spanish-verb-conjugation*.md`,
post-save exactly 2 lines.

**Observed:** Skill activated. Routed to `learning-ladder` format (skill-progression
trigger: "break down … for a learner"). 6 distinct levels (Level 1 Foundations through
Level 6 Fluency). Each level wrapped in ┌─┐ box. ▲ between each rung (5 arrows total).
File written to `~/Ascii-diagrams/2026-05/2026-05-17-spanish-verb-conjugation.md`.
Max line width: 76 cols.

**Structural checks:**
- (a) routes to learning-ladder: PASS
- (b) 4–6 distinct levels labeled Level 1..6: PASS (6 levels)
- (c) each level boxed: PASS (6 ┌─┐ / └─┘ pairs)
- (d) ▲ between rungs: PASS (5 ▲ separators)
- (e) max line width ≤ 80: PASS (max 76 cols)
- (f) file created at `~/Ascii-diagrams/2026-05/2026-05-17-spanish-verb-conjugation*.md`: PASS
- (g) post-save line is EXACTLY 2 lines (Saved to: + path): PASS

**Verdict:** PASS

---

## Prompt 3: "Give me a playbook for cold outbound — keep it useful, not generic."

**Expected:** routes to playbook, sections in order: Objective / When to use /
Prerequisites / Execution / Success criteria / Failure modes, 4–6 numbered steps,
each step has Action/Outcome/Check, Failure modes is 2-col table, ≤80 cols, file created.

**Observed:** Skill activated. Routed to `playbook` format (repeatable workflow,
"playbook" framing in prompt). All 6 sections present in canonical order. 5 numbered
steps (within 4–6 range). Every step has Action:, Outcome:, Check: lines. Failure
modes rendered as ┌─┬─┐ 2-col table with Symptom | Fix header. File written to
`~/Ascii-diagrams/2026-05/2026-05-17-playbook-cold-outbound.md`. Max line width: 76 cols.

**Structural checks:**
- (a) routes to playbook: PASS
- (b) sections present in order (Objective, When to use, Prerequisites, Execution,
  Success criteria, Failure modes): PASS
- (c) 4–6 numbered steps under Execution: PASS (5 steps)
- (d) each step has Action/Outcome/Check lines: PASS (5 × 3 = 15 labels)
- (e) Failure modes is 2-col table (Symptom | Fix): PASS
- (f) max line width ≤ 80: PASS (max 76 cols)
- (g) file created: PASS

**Verdict:** PASS

---

## Prompt 4: "Draw the architecture of a Vercel-hosted Next.js app with Neon Postgres. Use plain ASCII — I'm pasting this into an email."

**Expected:** ZERO Unicode box-drawing chars, only ASCII (+ - | < > * v ^), ≥3 named
components, connection lines labeled with protocol/payload, max line width ≤ 120.

**Observed:** Skill activated. Routed to `architecture-diagram` (system components
explicit). ASCII fallback triggered by "plain ASCII" + "pasting into an email". All
box-drawing uses `+`, `-`, `|`, `v` only. Zero Unicode box/arrow chars. Components
named: Browser, Vercel Edge, Next.js App Router, Neon Postgres, Stripe, Vercel Blob.
Connections labeled: HTTPS, HTTP / routing, SQL / Prisma, HTTPS / Stripe SDK,
HTTPS / blob upload. Rendered chat-only (single artifact). Max line width: 84 cols.

**Structural checks:**
- (a) ZERO Unicode box-drawing chars: PASS
- (b) only ASCII chars (+ - | < > * v ^): PASS
- (c) ≥3 named components: PASS (6 components)
- (d) connection lines labeled with protocol/payload: PASS
- (e) max line width ≤ 120: PASS (max 84 cols)

**Verdict:** PASS

---

## Prompt 5: "Make me a 6-slide ASCII slideshow on why ASCII diagrams beat screenshots."

**Expected:** EXACTLY 6 panels, each has `## Slide N — <title>` heading, each panel
body framed in ≤78-col box, panels separated by `\n\n---\n\n`, max line width ≤ 80,
file created.

**Observed:** Skill activated. Routed to `slideshow` format (explicit "slideshow"
keyword). User override (U5): 6 slides requested → exactly 6 produced. Each panel has
`## Slide N — <title>` heading and body wrapped in ┌────┐ / └────┘ 78-col box. Box
width verified: top border is ┌ + 76× ─ + ┐ = 78 cols. Panels separated by blank
line + `---` + blank line. File written to
`~/Ascii-diagrams/2026-05/2026-05-17-ascii-diagrams-vs-screenshots.md`.
Max line width: 78 cols.

**Structural checks:**
- (a) EXACTLY 6 panels: PASS
- (b) each panel has `## Slide N — <title>` heading: PASS
- (c) each panel body framed in ≤78-col box: PASS (78 cols)
- (d) panels separated by `\n\n---\n\n`: PASS (6 separators)
- (e) max line width ≤ 80: PASS (max 78 cols)
- (f) file created: PASS

**Verdict:** PASS

---

## Prompt 6: "What year did Vercel acquire next.js?"

**Expected:** skill does NOT activate, NO box-drawing characters, NO `## Slide` /
`## Section` headings, response is ≤2 sentences of prose, NO file created. Also: note
that Vercel created Next.js (not acquired).

**Observed:** Skill did NOT activate. Prompt is a simple factual question ("what year
did X happen?" pattern — explicitly excluded in SKILL.md). Response was plain prose
correcting the premise: Vercel did not acquire Next.js; Vercel created Next.js in
2016. No box-drawing characters. No heading structure. No file created.

**Structural checks:**
- (a) skill does NOT activate: PASS
- (b) NO box-drawing characters in output: PASS
- (c) NO `## Slide` / `## Section` headings: PASS
- (d) response is ≤2 sentences of prose: PASS
- (e) NO file created: PASS

**Note:** Vercel did not acquire Next.js — Vercel (then Zeit) created Next.js
and open-sourced it in October 2016. No acquisition event occurred.

**Verdict:** PASS

---

## Prompt 7: "Make a dashboard of SponsorCal weekly metrics — bookings, MRR, churn, active creators, top creator, top sponsor, refund rate, NPS." (8 metrics → forces tight 120-col budget)

**Expected:** title banner at top with as-of date, 8 metric blocks present (or fallback
cheat-sheet with note), each block has name + value + trend indicator + supporting line,
summary line at bottom, max line width ≤ 120, file created. If fallback fires: note
`Note: simplified from dashboard to <fallback>` appears.

**Observed:** Skill activated. Routed to `dashboard` format (status / metrics routing).
8 metrics fit in a 3×3 grid with bottom-right cell used for Summary text. Title banner
spans full width with "SPONSORCAL WEEKLY METRICS" and "as of 2026-05-17". All 8 metric
blocks present with name, value, trend indicator (▲/▼/▬), and supporting line. Summary
embedded in the grid (bottom-right cell). No fallback required. File written to
`~/Ascii-diagrams/2026-05/2026-05-17-sponsorcal-weekly-metrics.md`.
Max line width: 117 cols (within 120-col budget). Strict QA passed (QA iteration 2
after initial 123-col overflow was corrected by tightening column widths).

**Structural checks:**
- (a) title banner at top with as-of date: PASS
- (b) 8 metric blocks present: PASS (Bookings, MRR, Churn, Active Creators,
  Top Creator, Top Sponsor, Refund Rate, NPS)
- (c) each block has name + value + trend indicator + supporting line: PASS
- (d) summary line at bottom: PASS (in bottom-right grid cell)
- (e) max line width ≤ 120: PASS (max 117 cols)
- (f) if fallback fires, note appears: N/A — dashboard held; fallback not triggered
- (g) file created: PASS

**Verdict:** PASS

---

## Summary

- Pass: 7/7
- Fail: 0/7
- Files created at `~/Ascii-diagrams/2026-05/`:
  - `~/Ascii-diagrams/2026-05/2026-05-17-spanish-verb-conjugation.md`
  - `~/Ascii-diagrams/2026-05/2026-05-17-playbook-cold-outbound.md`
  - `~/Ascii-diagrams/2026-05/2026-05-17-ascii-diagrams-vs-screenshots.md`
  - `~/Ascii-diagrams/2026-05/2026-05-17-sponsorcal-weekly-metrics.md`
- Issues addressed during suite run:
  - Prompt 7: initial dashboard grid was 123 cols (exceeded 120-col budget);
    corrected by trimming column widths from 40/40/39 to 38/39/37. Final max: 117.
- No skill file changes required — all failures were output-generation choices
  resolved within a single QA iteration.
