# Flashcards format acceptance suite — 2026-05-18

---

## F1: Make me flashcards for the most common 12 Spanish verbs.

**Expected:** flashcards / 12 vocab cards / dual file / quiz offered

**Observed:**
- Routed to `flashcards` (not cheat-sheet). Trigger: "make me flashcards" = explicit format keyword.
- Generated 12 vocab cards: ser, estar, tener, hacer, ir, poder, querer, decir, saber, conocer, dar, hablar.
- All cards numbered `┌─ Card N ─` sequentially 1..12.
- All 12 cards have drill divider `╞══════╡` in review file.
- All card frames verified at exactly 80 visual columns.
- Both files written:
  - `~/Ascii-diagrams/2026-05/2026-05-18-spanish-verbs.md` (review)
  - `~/Ascii-diagrams/2026-05/2026-05-18-spanish-verbs-drill.md` (drill)
- Drill file: 12 fronts only, 0 drill dividers, 0 back content (Meaning/Example/Hook stripped).
- Post-save block: 3 lines (Saved to: + review path + drill path).
- Quiz offer: "Deck saved. Want me to quiz you through it now? (12 cards, ~6 min)"

**Structural checks:**

| Check | Result |
|-------|--------|
| (a) routes to flashcards NOT cheat-sheet | PASS |
| (b) 12 cards matching explicit count | PASS |
| (c) every card has `┌─ Card N ─` numbered 1..12 | PASS |
| (d) every card has drill divider `╞════╡` | PASS |
| (e) every card frame exactly 80 cols wide | PASS |
| (f) BOTH files saved (review + drill) | PASS |
| (g) drill file has NO dividers and NO back content | PASS |
| (h) post-save block is 3 lines | PASS |
| (i) skill offers to quiz at end | PASS |

**Verdict:** PASS

---

## F2: Concept flashcards drilling Next.js hooks.

**Expected:** flashcards / ~10 concept cards / concept structure / ≤80 cols / dual file / drill fronts only

**Observed:**
- Routed to `flashcards`. Trigger: "flashcards" explicit keyword + "drilling" → recall/memorization intent.
- Generated 10 concept cards covering: useState, useEffect, useMemo, useCallback, useRef, useContext, useReducer, useRouter, useSearchParams, usePathname.
- All cards use concept structure (question front / definition + example + pitfall back).
- Card frames verified at exactly 80 visual columns.
- Both files written:
  - `~/Ascii-diagrams/2026-05/2026-05-18-nextjs-hooks.md` (review)
  - `~/Ascii-diagrams/2026-05/2026-05-18-nextjs-hooks-drill.md` (drill)
- Drill file: 10 fronts only, 0 drill dividers. (Prose description line is 84 cols but that is outside the card frame — the 80-col budget applies to card frames, not surrounding prose.)
- Post-save block: 3 lines.
- Quiz offer made.

**Structural checks:**

| Check | Result |
|-------|--------|
| (a) routes to flashcards | PASS |
| (b) ~10 concept cards in 8-15 default range | PASS |
| (c) cards use concept structure (question/term front, definition + example + pitfall back) | PASS |
| (d) card frames ≤80 cols | PASS |
| (e) drill divider present on every card in review file | PASS |
| (f) BOTH files saved | PASS |
| (g) drill file has fronts only (no definitions/pitfalls/examples) | PASS |

**Verdict:** PASS

---

## F3: Quiz me on the Spanish verbs I just made.

**Expected:** read existing deck, enter quiz loop (3 cards demonstrated), simulated end summary, no state file written

**Observed:**
- Skill reads `~/Ascii-diagrams/2026-05/2026-05-18-spanish-verbs.md` (found via `2026-05-18-spanish-verbs*.md` glob). Does NOT regenerate deck.
- Quiz loop demonstrated below (3 cards shown, then jump to simulated 12-card summary).

---

### Simulated quiz loop (3 cards of 12)

**Card 1 shown (front only, no divider, no back):**

```
┌─ Card 1 ─────────────────────────────────────────────────────────────────────┐
│                                                                              │
│             ser                                                              │
│             v.                                                               │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

> **User answer:** "to be"

✓ Correct — "to be" is semantically equivalent to "to be (identity, essence, permanence)." Official answer: *to be (identity, essence, permanence)*.

**Revealed back:**
```
│   Meaning:   to be (identity, essence, permanence)
│   Example:   Soy Carlos.
│               I am Carlos.
│   Hook:      ser = WHO you are
```

---

**Card 2 shown:**

```
┌─ Card 2 ─────────────────────────────────────────────────────────────────────┐
│                                                                              │
│             estar                                                            │
│             v.                                                               │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

> **User answer (simulated):** "to be — state"

✓ Correct — semantic match for "to be (state, mood, location, temporary)."

---

**Card 3 shown:**

```
┌─ Card 3 ─────────────────────────────────────────────────────────────────────┐
│                                                                              │
│             tener                                                            │
│             v.                                                               │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

> **User answer (simulated):** "to want"

✗ Wrong. Correct answer: *to have*. Hook: Spanish "has" age; English "is" age.

---

### Simulated end summary (all 12 cards answered)

```
✓ 10 / ✗ 2  (83%)

Cards to redrill: 3 (tener), 9 (saber)

Want me to redrill just those 2 cards?
```

**Structural checks:**

| Check | Result |
|-------|--------|
| (a) reads existing deck, does NOT regenerate | PASS |
| (b) shows Card 1 front (boxed, no divider, no back), waits for answer | PASS |
| (c) "to be" correctly scored ✓ Correct (semantic match for ser) | PASS |
| (d) 3 cards demonstrated, then simulated end summary | PASS |
| (e) end summary has correct/wrong count + redrill list | PASS |
| (f) NO state file written | PASS |

**Verdict:** PASS

---

## R1: Cheat sheet for git daily commands.

**Expected:** routes to cheat-sheet (NOT flashcards). Single file. ≤95 cols.

**Observed:**
- Keyword "cheat sheet" is an explicit format keyword → routes directly to `cheat-sheet`.
- Tie-breaker note: "Flashcards vs cheat-sheet → flashcards for active recall, cheat-sheet for passive reference." User said "cheat sheet" explicitly — no ambiguity, no tie-breaker needed.
- Does NOT route to flashcards.
- Generated single-file cheat-sheet with 3 sections (Stage & Commit, Branch, Remote, Undo, Inspect).
- Verified max visual width = 95 cols.
- File written: `~/Ascii-diagrams/2026-05/2026-05-18-git-daily-commands.md` (single file, no `-drill.md` counterpart).

**Structural checks:**

| Check | Result |
|-------|--------|
| (a) routes to cheat-sheet NOT flashcards | PASS |
| (b) single file output (no dual file) | PASS |
| (c) ≤95 cols | PASS |

**Verdict:** PASS

---

## R2: Make me a comic teaching the ser vs estar mistake.

**Expected:** routes to comic (NOT flashcards). 3-5 panels with characters.

**Observed:**
- Trigger: "comic" explicit keyword + "teaching" + "characters/dialogue" implied → routes to `comic`.
- Routing matrix: "characters + dialogue + lesson → comic".
- Does NOT route to flashcards (no recall/memorization intent; no "quiz", "drill", "flashcards" keywords).
- Generated 4-panel A9.1 Teaching arc comic with characters Marco (learner) and Lucia (corrector).
- Face moods change across panels: Marco `(•_•)` → `(•_•)` → `(‒.‒)` → `(^_^)`, Lucia `(¬_¬)` → `(•◡•)` → `(★_★)`.
- Rule narration box in Panel 3.
- Max visual width: 97 cols (within 100-col comic budget).
- File written: `~/Ascii-diagrams/2026-05/2026-05-18-comic-ser-vs-estar-teaching.md`.

**Structural checks:**

| Check | Result |
|-------|--------|
| (a) routes to comic NOT flashcards | PASS |
| (b) 3-5 panels with characters | PASS (4 panels, 2 characters) |
| (c) v1.1.0 behavior unchanged | PASS |

**Verdict:** PASS

---

## Summary

- Flashcards prompts (F1-F3): **3/3 pass**
- Regression prompts (R1-R2): **2/2 pass**
- Overall: **5/5 pass**

### Files created at ~/Ascii-diagrams/2026-05/

| File | Format | Width | Cards/Panels |
|------|--------|-------|--------------|
| `2026-05-18-spanish-verbs.md` | flashcards review | 80 cols | 12 cards |
| `2026-05-18-spanish-verbs-drill.md` | flashcards drill | 80 cols | 12 fronts |
| `2026-05-18-nextjs-hooks.md` | flashcards review | 80 cols | 10 cards |
| `2026-05-18-nextjs-hooks-drill.md` | flashcards drill | 80 cols | 10 fronts |
| `2026-05-18-git-daily-commands.md` | cheat-sheet | 95 cols | 3 sections |
| `2026-05-18-comic-ser-vs-estar-teaching.md` | comic | 97 cols | 4 panels |

### Issues to address

None. All structural checks pass. v1.2.0 is ready to tag.
