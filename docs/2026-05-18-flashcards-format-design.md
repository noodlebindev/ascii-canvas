# Flashcards format — Design Spec (v1.2.0)

**Date:** 2026-05-18
**Status:** Spec — ready for implementation plan
**Skill version bump:** v1.1.0 → v1.2.0 (additive — no breaking changes)
**Spec location:** `~/Skills/ascii-canvas/docs/2026-05-18-flashcards-format-design.md`

---

## 1. Purpose

Add `flashcards` as the 18th format in the ascii-canvas catalog. Compose ASCII flashcard decks for active recall study — vocab + concept cards with a folded layout that supports both passive review (single-file glance) and active self-testing (separate drill file + optional in-chat quiz).

**Two card subtypes:** vocab and concept. Mixed-subtype decks allowed.

## 2. Scope

**In scope (v1.2.0):**
- New format file: `formats/flashcards.md`
- New example file: `examples/flashcards-example.md`
- New entry in `composition-rules/narrative-arcs.md`: A10 deck arc (no narrative arc — card count guidance only)
- New width-budget entry: `flashcards` → 80 cols
- SKILL.md description + routing matrix updates
- QA additions specific to flashcards in `composition-rules/qa-checklist.md`
- Dual file output (review + drill)
- Opt-in in-chat quiz mode (per-session scoring, no persistence)
- Version tag bump to `v1.2.0`

**Out of scope (deferred to future):**
- Spaced repetition scheduling / cross-session state
- Card difficulty markers (★ / ★★ / ★★★)
- Card categories or tags within a deck
- Images, audio
- Cloze (fill-in-the-blank) cards
- Multiple-choice cards
- Bidirectional card auto-generation (English↔Spanish from one definition)
- Quiz score persistence across sessions

## 3. Architecture

**File additions:**
```
~/Skills/ascii-canvas/
├── formats/
│   └── flashcards.md          ← NEW
├── composition-rules/
│   ├── narrative-arcs.md      ← UPDATE: add A10 deck arc
│   ├── width-budgets.md       ← UPDATE: add flashcards = 80 cols
│   └── qa-checklist.md        ← UPDATE: add flashcards-specific QA + cheat-sheet fallback
├── examples/
│   └── flashcards-example.md  ← NEW
├── SKILL.md                   ← UPDATE: trigger keywords + routing matrix
└── docs/
    └── 2026-05-18-flashcards-format-design.md   ← this spec
```

**No file removals or restructures.** All changes additive.

**Format catalog count:** 17 → 18.

## 4. Card frame grammar

Every card is a 78-col-wide framed box (1-col padding each side of the 80-col budget) with a thick **drill divider** at the midpoint:

```
┌─ Card N ──────────────────────────────────────────────────────────────────────┐
│                                                                                │
│   <FRONT content>                                                              │
│                                                                                │
╞════════════════════════════════════════════════════════════════════════════════╡
│                                                                                │
│   <BACK content>                                                               │
│                                                                                │
└────────────────────────────────────────────────────────────────────────────────┘
```

**Rules:**
- Card title: `┌─ Card N ─` always numbered, deck-wide sequential (1, 2, 3, …)
- Drill divider: `╞═══...═══╡` heavy double line — the one allowed line-weight switch inside a card (box-drawing.md R3 exception)
- Card outer frame uses light box-drawing (`┌─┐│└─┘`)
- Cards separated by `\n\n` (one blank line). No `---` between cards
- Card body cap: back side ≤ 5 lines of content. Overflow → split into two cards.

## 5. Vocab card structure

```
┌─ Card N ──────────────────────────────────────────────────────────────────────┐
│                                                                                │
│             <term>                                                             │
│             [optional: pronunciation guide]                                    │
│             [optional: part of speech — n. / v. / adj. / adv.]                 │
│                                                                                │
╞════════════════════════════════════════════════════════════════════════════════╡
│                                                                                │
│   Meaning:   <translation / one-line definition>                               │
│   Example:   <example sentence in source language>                             │
│               <English gloss of the example>                                   │
│   Hook:      <mnemonic / memory hook>  [optional]                              │
│                                                                                │
└────────────────────────────────────────────────────────────────────────────────┘
```

**Front fields:**
- **Term/word** (required) — center-or-left-aligned
- **Pronunciation** (optional) — IPA `[ˈser]` or romanized hint
- **Part of speech** (optional) — short abbreviation

**Back fields:**
- **Meaning** (required) — translation or short definition
- **Example** (required) — 2 lines (source language + English gloss)
- **Hook** (optional) — memory hook / mnemonic

## 6. Concept card structure

```
┌─ Card N ──────────────────────────────────────────────────────────────────────┐
│                                                                                │
│   <term or short question>                                                     │
│                                                                                │
╞════════════════════════════════════════════════════════════════════════════════╡
│                                                                                │
│   <definition — 1-3 lines>                                                     │
│   Example: <key example or analogy>  [optional]                                │
│   Pitfall: <common mistake>  [optional]                                        │
│                                                                                │
└────────────────────────────────────────────────────────────────────────────────┘
```

**Front fields:**
- **Term or short question** (required) — 1-2 lines max
- No part-of-speech or pronunciation (concept cards aren't vocab)

**Back fields:**
- **Definition** (required) — 1-3 lines
- **Example/analogy** (optional)
- **Pitfall** (optional) — common mistake to flag

## 7. Mixed-subtype decks

A single deck may interleave vocab and concept cards. Each card stands alone — there's no enforced subtype ordering or grouping. Example:

```
Card 1 (vocab):    estar         → to be (state)
Card 2 (vocab):    ser           → to be (identity)
Card 3 (concept):  ser vs estar  → use ser for permanent, estar for temporary
Card 4 (vocab):    tener         → to have
Card 5 (concept):  tener for age → "Tengo 30 años" not "Soy 30"
```

The format file's authoring guidance recommends grouping related cards but doesn't enforce it.

## 8. A10 — Deck arc (added to narrative-arcs.md)

Flashcards have no narrative arc in the traditional sense — there's no "hook → reveal → application." The A10 entry in `narrative-arcs.md` is purely card-count guidance:

- **Default card count:** 8–15 cards (one focused study session)
- **Never exceed 30 cards** in a single deck without explicit user request
- **If topic needs more than 30:** split into themed sub-decks (`spanish-verbs-present`, `spanish-verbs-past`, etc.)
- **Compress before expanding:** if you can teach the concept in fewer cards, do
- **Universal U1 applies:** every card must earn its existence; no filler cards

## 9. Width budget

**80 cols** — added to `composition-rules/width-budgets.md`.

Mobile-friendly and printable on standard letter paper without resizing. Cards sized at exactly 80 cols outer frame.

## 10. Dual file output

Per Q2 option D (folded layout + drill file):

### 10.1 Review file (full deck)

Path: `~/Ascii-diagrams/YYYY-MM/YYYY-MM-DD-<slug>.md`

Structure:
```markdown
# <Topic>

<1-2 line description of deck>

---

<Card 1 — full folded layout with front + drill divider + back>

<Card 2 — full folded layout>

...

<Card N — full folded layout>
```

### 10.2 Drill file (fronts only)

Path: `~/Ascii-diagrams/YYYY-MM/YYYY-MM-DD-<slug>-drill.md`

Structure:
```markdown
# <Topic> — drill mode

<N> cards. Try to recall each card's answer. Then open `<slug>.md` to check.

---

<Card 1 — fronts only, no drill divider, no back, but frame closed normally>

<Card 2 — fronts only>

...

<Card N — fronts only>
```

In the drill file, each card is a smaller frame (just the front content) — no drill divider needed because there's no back to hide. Card numbers match between review and drill files.

### 10.3 Post-save block (3 lines instead of standard 2)

```
Saved to:
~/Ascii-diagrams/YYYY-MM/YYYY-MM-DD-<slug>.md         (review)
~/Ascii-diagrams/YYYY-MM/YYYY-MM-DD-<slug>-drill.md   (drill)
```

### 10.4 Slug naming

- Topic-driven, lowercase, hyphen-separated, 4–6 words
- Examples: `spanish-verbs`, `nextjs-hooks`, `latin-cooking-vocab`
- Fallback if intent unclear: `flashcards-<short-topic>`

## 11. Chat quiz mode (opt-in)

**After both files are saved,** the skill offers in chat:

> "Deck saved. Want me to quiz you through it now? (<N> cards, ~<estimate> min)"

Time estimate: ~30 seconds per card.

### 11.1 If user says yes — quiz loop

For each card 1..N:

1. Show the card's **front only** inside the card frame (no drill divider, no back content)
2. Wait for user's answer
3. Compare user's answer to the card's back:
   - **Exact match (case-insensitive):** mark ✓ Correct
   - **Semantic equivalent:** mark ✓ Correct, with a brief note on the "official" answer
   - **Wrong or partial:** mark ✗, reveal the correct back content
4. Move to next card

### 11.2 End-of-quiz summary

```
✓ <N correct> / ✗ <M missed>  (<percentage>%)

Cards to redrill: <list of card numbers missed, or "none — perfect score">

Want me to redrill just those <M> cards?
```

### 11.3 Quiz behavior rules (encoded in formats/flashcards.md)

- **Reveal back card-by-card** — never preview the back before the user answers
- **Generous on semantic matches:** "to be (state)" and "to be — state" both count as correct
- **Strict on conjugation:** if user says "tengo" for the front "tú have," they're wrong (it's "tienes")
- **No persistent state** — session-only scoring. No `.drill-state.json` file. No cross-session memory.
- **Always offer redrill at end** — never auto-restart
- **Quiz can be ended early** — user typing "stop" / "quit" / "done" exits the loop with a partial summary

### 11.4 If user says no to quiz

Skill responds with just the post-save block (review + drill paths) and ends the turn.

## 12. SKILL.md updates

### 12.1 Description / trigger keywords

Add to the SKILL.md frontmatter `description` field and the "Fire on:" bullet list:
- "make flashcards", "flashcard deck", "vocab cards", "study cards", "Anki-style cards"
- "drill me on X", "quiz me on X", "test me on X", "help me memorize X"

### 12.2 Routing matrix additions

Add two new rows under "CHOOSE FORMAT" section in SKILL.md:
```
recall / memorization drill         → flashcards
quiz / test self                    → flashcards
```

### 12.3 Tie-breaker additions

- Flashcards vs cheat-sheet ambiguous → flashcards if active recall implied ("drill", "memorize", "test"), cheat-sheet if passive reference ("look up", "reference for")
- Flashcards vs comparison-table → comparison-table for side-by-side comparison of fixed options, flashcards for sequential Q/A recall

## 13. QA additions

In `composition-rules/qa-checklist.md`, add a new subsection "Flashcards-specific strict QA" after the comic-specific section.

Flashcards artifacts run the standard 8-point checklist PLUS:

1. **Every card has a card number** (`┌─ Card N ─`) and numbers are sequential 1..N
2. **Drill divider present on every card in the review file** (`╞════╡`)
3. **Drill file has NO drill divider** and NO back content — fronts only
4. **Card subtype consistency** — each card is either vocab structure or concept structure; no half-mixed cards (vocab front with concept back)
5. **Back side ≤ 5 lines of content** (excluding padding and borders)
6. **Card frame widths identical** — every card in a deck is exactly 80 cols outer width
7. **Drill file card count = review file card count** — same N cards, same numbering, just no backs
8. **Front content fits without wrapping** — terms/questions short enough to render on one line; multi-line fronts allowed only for concept cards with explicit multi-line questions

### 13.1 Format fallback addition

Add to the fallback map in `qa-checklist.md`:
```
| flashcards | cheat-sheet |
```

Reason: if a flashcards request can't be made coherent (topic has no discrete recall-able items, or items are too complex to fit a card's back-side cap), fall back to a flat cheat-sheet reference.

## 14. Save behavior summary

- **Always auto-save both files** (review + drill) when the skill produces a flashcards artifact
- **No single-file flashcards mode** — even a 3-card deck saves both files
- **Inherits existing iteration guard** — if user signaled "draft" / "try again," chat-only (no save). On confirmation, save both files.

## 15. Example file content

`examples/flashcards-example.md` ships with a richer reference artifact. Suggested topic:

**Topic:** Spanish verbs — 10 mixed cards (5 vocab + 5 concept), demonstrating both subtypes interleaved. Includes ser, estar, tener, hacer, gustar as vocab; ser-vs-estar, tener-for-age, gustar-inverse-construction as concept cards.

The example shows the FULL review file (folded layout) and notes that the drill file would be a separate auto-generated version with backs removed.

## 16. Build sequence

1. Update `composition-rules/narrative-arcs.md` — add A10 deck arc
2. Update `composition-rules/width-budgets.md` — add `flashcards = 80`
3. Update `composition-rules/qa-checklist.md` — add flashcards-specific QA + cheat-sheet fallback
4. Write `formats/flashcards.md` (full format file including quiz behavior rules)
5. Write `examples/flashcards-example.md` (10-card mixed deck)
6. Update `SKILL.md` — description + routing matrix + tie-breakers
7. Run acceptance suite: 3 flashcards-specific prompts + spot-check 2 existing prompts (regression)
8. Tag `v1.2.0`

## 17. Acceptance criteria

The format is v1.2.0-complete when:

1. All 6 files (1 new format, 1 new example, 3 updated composition-rules, 1 updated SKILL.md) committed
2. v1.0.0 and v1.1.0 acceptance suites still pass (no regressions)
3. Three new flashcards-specific acceptance prompts pass:
   - **F1:** "Make me flashcards for the most common 12 Spanish verbs." → 12 vocab cards, dual file saved, ≤80 cols, quiz offered at end
   - **F2:** "Concept flashcards drilling Next.js hooks." → ~10 concept cards (useState, useEffect, useMemo, useCallback, useRef, useContext, etc.), dual file saved, drill file has fronts only
   - **F3:** "Quiz me on the Spanish verbs I just made." → assuming F1's deck exists, skill enters quiz mode using that deck, scores per-session, emits redrill list at end
4. Strict QA catches: a deliberately malformed deck (e.g., card 3 missing the drill divider) → fail-twice → simplify or reroute to cheat-sheet
5. Repository tagged `v1.2.0`

## 18. Open items

None. All design decisions resolved during brainstorming Q1–Q6.
