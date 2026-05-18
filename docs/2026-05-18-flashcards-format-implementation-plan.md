# Flashcards Format (v1.2.0) Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add `flashcards` as the 18th format in the ascii-canvas skill, with vocab + concept card subtypes, folded layout (drill divider mid-card), dual file output (review + drill), and opt-in in-chat quiz mode with per-session scoring. Bump v1.1.0 → v1.2.0.

**Architecture:** Additive only. Three composition-rules files get updates, two new files are created (`formats/flashcards.md`, `examples/flashcards-example.md`), SKILL.md gets routing matrix + trigger keyword updates. No breaking changes to existing 17 formats.

**Tech Stack:** Markdown only. Git for version control. No build step. No external dependencies.

**Spec reference:** `/Users/priyeshpatel/Skills/ascii-canvas/docs/2026-05-18-flashcards-format-design.md`

**Verification model:** 3 flashcards-specific acceptance prompts + 2 regression prompts at the end.

---

## Conventions

- All paths absolute under `/Users/priyeshpatel/Skills/ascii-canvas/`.
- Every task ends with a focused commit using `feat:`, `docs:`, or `chore:` prefixes.
- Full content shown verbatim in each task — no "similar to Task N" references.

---

# Phase 1 — Composition rules updates

## Task 1: Add flashcards width budget

**Files:**
- Modify: `composition-rules/width-budgets.md`

- [ ] **Step 1: Insert flashcards row in the per-format budgets table**

Find the `## Per-format budgets` table. Add this row alongside the other 80-col formats (playbook, slideshow, step-by-step-guide, learning-ladder):

```markdown
| flashcards | 80 |
```

Recommended insertion point: right after `| playbook | 80 |`.

- [ ] **Step 2: Verify**

Run:
```bash
grep -c "^| flashcards" /Users/priyeshpatel/Skills/ascii-canvas/composition-rules/width-budgets.md
```
Expected: `1`

- [ ] **Step 3: Commit**

```bash
cd /Users/priyeshpatel/Skills/ascii-canvas && \
  git add composition-rules/width-budgets.md && \
  git commit -m "feat(flashcards): add 80-col width budget"
```

---

## Task 2: Add A10 deck arc to narrative-arcs.md

**Files:**
- Modify: `composition-rules/narrative-arcs.md`

- [ ] **Step 1: Locate the insertion point**

The file currently has arcs A1–A9 (with A9 being the comic-arc family). Insert A10 BETWEEN the closing of A9's "Comic-specific panel rules" section and `## Universal panel rules (apply to every arc)`.

- [ ] **Step 2: Insert A10 verbatim**

Add this content right before the `## Universal panel rules` heading:

````markdown
### A10 — Deck arc (flashcards format)

Flashcards have no narrative arc — there's no hook/reveal/application sequence. The A10 entry is purely card-count guidance for the flashcards format.

- **Default card count:** 8–15 cards (one focused study session)
- **Never exceed 30 cards** in a single deck without explicit user request
- **If topic needs more than 30:** split into themed sub-decks (`spanish-verbs-present`, `spanish-verbs-past`, etc.)
- **Compress before expanding:** if you can teach the concept in fewer cards, do
- **U1 applies:** every card must earn its existence; no filler cards

**Use for:** flashcards format only. Other formats use A1–A9.

````

- [ ] **Step 3: Verify**

Run:
```bash
grep -c "^### A10" /Users/priyeshpatel/Skills/ascii-canvas/composition-rules/narrative-arcs.md
```
Expected: `1`

Also verify the Universal panel rules heading still follows after A10:
```bash
grep -A1 "^### A10" /Users/priyeshpatel/Skills/ascii-canvas/composition-rules/narrative-arcs.md | head -5
```

- [ ] **Step 4: Commit**

```bash
cd /Users/priyeshpatel/Skills/ascii-canvas && \
  git add composition-rules/narrative-arcs.md && \
  git commit -m "feat(flashcards): add A10 deck arc"
```

---

## Task 3: Add flashcards-specific QA + fallback

**Files:**
- Modify: `composition-rules/qa-checklist.md`

- [ ] **Step 1: Add the flashcards-specific QA subsection**

Locate the existing `## Comic-specific strict QA` section. Insert the new flashcards-specific subsection AFTER comic's section ends and BEFORE the `## When QA runs` heading.

Insert verbatim:

````markdown
## Flashcards-specific strict QA (in addition to the 8 points + cross-artifact check)

When the artifact is a flashcards deck, strict QA additionally verifies:

1. **Every card has a card number** (`┌─ Card N ─`) and numbers are sequential 1..N
2. **Drill divider present** on every card in the review file (`╞════╡`)
3. **Drill file has NO drill divider** and NO back content — fronts only
4. **Card subtype consistency** — each card is either vocab structure (term + meaning + example) or concept structure (term/question + definition); no half-mixed cards
5. **Back side ≤ 5 lines of content** (excluding padding and borders)
6. **Card frame widths identical** — every card in a deck is exactly 80 cols outer width
7. **Drill file card count = review file card count** — same N cards, same numbering, just no backs
8. **Front content fits without wrapping** — terms/questions short enough to render on one line; multi-line fronts allowed only for concept cards with explicit multi-line questions

````

- [ ] **Step 2: Add flashcards row to the fallback map**

Find the `## Format fallback map (graceful degradation)` table. Add this row at the bottom of the existing table (after the `| comic | slideshow |` row added in v1.1.0):

```markdown
| flashcards | cheat-sheet |
```

- [ ] **Step 3: Verify**

Run:
```bash
grep -c "^## Flashcards-specific strict QA" /Users/priyeshpatel/Skills/ascii-canvas/composition-rules/qa-checklist.md
```
Expected: `1`

Run:
```bash
grep -c "^| flashcards | cheat-sheet |" /Users/priyeshpatel/Skills/ascii-canvas/composition-rules/qa-checklist.md
```
Expected: `1`

- [ ] **Step 4: Commit**

```bash
cd /Users/priyeshpatel/Skills/ascii-canvas && \
  git add composition-rules/qa-checklist.md && \
  git commit -m "feat(flashcards): add flashcards-specific strict QA + cheat-sheet fallback"
```

---

# Phase 2 — The format file

## Task 4: Write formats/flashcards.md

**Files:**
- Create: `/Users/priyeshpatel/Skills/ascii-canvas/formats/flashcards.md`

- [ ] **Step 1: Author the file with the full content below**

Write to `/Users/priyeshpatel/Skills/ascii-canvas/formats/flashcards.md`:

````markdown
# flashcards

## Purpose

Compose ASCII flashcard decks for active recall study — vocab + concept cards with a folded layout (front + drill divider + back) that supports passive review (review file) and active drilling (separate drill file with fronts only). Optional in-chat quiz mode for interactive testing.

## Use when

- The user wants to memorize discrete items (vocab, concepts, facts) through repeated recall
- "Make flashcards for X", "flashcard deck on X", "study cards for X"
- "Drill me on X", "quiz me on X", "test me on X", "help me memorize X"
- Active testing/recall is the goal — not passive reference

## Do NOT use when

- User wants a flat reference for lookup → use `cheat-sheet`
- User wants side-by-side comparison of fixed options → use `comparison-table`
- Topic has no discrete recall-able items → fall back to `cheat-sheet`
- The "items" are actually steps in a workflow → use `step-by-step-guide` or `playbook`

## Width budget

80 cols

## Arc

A10 — Deck arc (card-count guidance only, no narrative). See `composition-rules/narrative-arcs.md`.

- Default card count: 8–15 cards (one study session)
- Never exceed 30 cards without explicit user request
- If topic needs more: split into themed sub-decks

## Layout rules

- **Vertical strip** — cards stacked top-to-bottom, one per row
- **Card frame** uses light box-drawing `┌─┐│└─┘` for outer borders
- **Drill divider** uses heavy double line `╞═══╡` at the midpoint of each card (this is the one allowed line-weight switch inside a card, per box-drawing.md R3 exception)
- **Card title** at top-left: `┌─ Card N ─` — always numbered, sequential 1..N
- **Cards separated by `\n\n`** (one blank line). No `---` between cards.
- **Card body cap:** back side ≤ 5 lines of content. Overflow → split into two cards.
- **Mixed subtypes OK** — vocab cards and concept cards can be interleaved in one deck.

## Vocab card structure

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

## Concept card structure

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

## Dual file output

Flashcards always produces TWO files (auto-saved):

### Review file

Path: `~/Ascii-diagrams/YYYY-MM/YYYY-MM-DD-<slug>.md`

Structure:
```markdown
# <Topic>

<1-2 line deck description>

---

<Card 1 — full folded layout>

<Card 2 — full folded layout>

...
```

### Drill file

Path: `~/Ascii-diagrams/YYYY-MM/YYYY-MM-DD-<slug>-drill.md`

Same cards but back side removed. Cards in the drill file have a smaller frame — just front content, no drill divider, no back:

```markdown
# <Topic> — drill mode

<N> cards. Try to recall each card's answer. Then open `<slug>.md` to check.

---

┌─ Card 1 ──────────────────────────────────────────────────────────────────────┐
│                                                                                │
│             <front content only>                                               │
│                                                                                │
└────────────────────────────────────────────────────────────────────────────────┘

┌─ Card 2 ──────────────────────────────────────────────────────────────────────┐
...
```

### Post-save block (3 lines)

```
Saved to:
~/Ascii-diagrams/YYYY-MM/YYYY-MM-DD-<slug>.md         (review)
~/Ascii-diagrams/YYYY-MM/YYYY-MM-DD-<slug>-drill.md   (drill)
```

### Slug naming

- Topic-driven, lowercase, hyphen-separated, 4–6 words
- Examples: `spanish-verbs`, `nextjs-hooks`, `latin-cooking-vocab`
- Fallback: `flashcards-<short-topic>`

## Chat quiz mode (opt-in)

After both files are saved, offer in chat:

> "Deck saved. Want me to quiz you through it now? (<N> cards, ~<N/2> min)"

### If user says yes — quiz loop

For each card 1..N:
1. Show the card's FRONT inside a card frame (no drill divider, no back content)
2. Wait for user's answer
3. Compare user's answer to the card's back:
   - Exact match (case-insensitive) → mark ✓ Correct
   - Semantic equivalent → mark ✓ Correct, brief note on the "official" answer
   - Wrong or partial → mark ✗, reveal the correct back content
4. Move to next card

### End-of-quiz summary

```
✓ <N correct> / ✗ <M missed>  (<percentage>%)

Cards to redrill: <list of card numbers missed, or "none — perfect score">

Want me to redrill just those <M> cards?
```

### Quiz behavior rules

- **Reveal back card-by-card** — never preview the back before the user answers
- **Generous on semantic matches:** "to be (state)" and "to be — state" both count as correct
- **Strict on conjugation:** if user says "tengo" for the front "tú have," they're wrong (it's "tienes")
- **No persistent state** — session-only scoring. No state file. No cross-session memory.
- **Always offer redrill at end** — never auto-restart
- **Quiz can be ended early** — user typing "stop" / "quit" / "done" exits with a partial summary
- **If user already has a deck file from a previous turn** and says "quiz me on the Spanish verbs I just made" — read the existing deck file from `~/Ascii-diagrams/` and start the quiz loop without regenerating

### If user says no

Skill responds with just the post-save block and ends the turn.

## Canonical skeleton — review file (5-card deck, 2 vocab + 3 concept)

```
# Spanish — top 5 verbs

5-card mixed deck (vocab + concept) covering ser, estar, tener, and the
ser-vs-estar contrast.

---

┌─ Card 1 ──────────────────────────────────────────────────────────────────────┐
│                                                                                │
│             ser                                                                │
│             v.                                                                 │
│                                                                                │
╞════════════════════════════════════════════════════════════════════════════════╡
│                                                                                │
│   Meaning:   to be (identity, essence, permanence)                             │
│   Example:   Soy Carlos.                                                       │
│               I am Carlos.                                                     │
│   Hook:      ser = WHO you are                                                 │
│                                                                                │
└────────────────────────────────────────────────────────────────────────────────┘

┌─ Card 2 ──────────────────────────────────────────────────────────────────────┐
│                                                                                │
│             estar                                                              │
│             v.                                                                 │
│                                                                                │
╞════════════════════════════════════════════════════════════════════════════════╡
│                                                                                │
│   Meaning:   to be (state, mood, location, temporary)                          │
│   Example:   Estoy cansado.                                                    │
│               I am tired.                                                      │
│   Hook:      estar = HOW you are                                               │
│                                                                                │
└────────────────────────────────────────────────────────────────────────────────┘

┌─ Card 3 ──────────────────────────────────────────────────────────────────────┐
│                                                                                │
│   When to use ser vs estar?                                                    │
│                                                                                │
╞════════════════════════════════════════════════════════════════════════════════╡
│                                                                                │
│   ser = identity / origin / permanent traits / time                            │
│   estar = location / mood / temporary state / ongoing action                   │
│   Example:  Es aburrido (boring person) vs Está aburrido (bored now)           │
│   Pitfall:  Don't use ser for "how I feel today" — that's estar                │
│                                                                                │
└────────────────────────────────────────────────────────────────────────────────┘
```

## Short rendered example — drill file (matching 3 cards, fronts only)

```
# Spanish — top 5 verbs — drill mode

5 cards. Try to recall each card's answer. Then open
`2026-05-18-spanish-top-5-verbs.md` to check.

---

┌─ Card 1 ──────────────────────────────────────────────────────────────────────┐
│                                                                                │
│             ser                                                                │
│             v.                                                                 │
│                                                                                │
└────────────────────────────────────────────────────────────────────────────────┘

┌─ Card 2 ──────────────────────────────────────────────────────────────────────┐
│                                                                                │
│             estar                                                              │
│             v.                                                                 │
│                                                                                │
└────────────────────────────────────────────────────────────────────────────────┘

┌─ Card 3 ──────────────────────────────────────────────────────────────────────┐
│                                                                                │
│   When to use ser vs estar?                                                    │
│                                                                                │
└────────────────────────────────────────────────────────────────────────────────┘
```

## Failure modes

- If the topic has no discrete recall-able items → fall back to `cheat-sheet`
- If a card's back overflows 5 lines → split into two cards (e.g., card 5 "ser uses" splits into 5a "ser for identity" and 5b "ser for time/origin")
- If width overflows at 80 cols → shorten term, abbreviate meaning, or drop optional fields (pronunciation, hook)
- If user requests >30 cards in one deck → split into themed sub-decks; offer "I'll make 3 separate decks: present-tense, past-tense, subjunctive"
- If the same term appears twice → consolidate or split into different facets (one card per facet)
- If user wants spaced-repetition tracking → out of scope in v1.2; suggest manual rotation through the drill file or external tool (Anki)
````

- [ ] **Step 2: Verify width**

Run:
```bash
python3 -c "
import re
c = open('/Users/priyeshpatel/Skills/ascii-canvas/formats/flashcards.md').read()
blocks = re.findall(r'\`\`\`[a-z]*\n(.*?)\`\`\`', c, re.DOTALL)
for i, b in enumerate(blocks, 1):
    w = max(len(l) for l in b.split('\n')) if b.strip() else 0
    print(f'block {i}: width {w}/80')
"
```
Expected: every block ≤ 80. Fix and re-verify if any exceed.

- [ ] **Step 3: Verify section structure**

Run:
```bash
grep -c "^## " /Users/priyeshpatel/Skills/ascii-canvas/formats/flashcards.md
```
Expected: `12` — Purpose, Use when, Do NOT use when, Width budget, Arc, Layout rules, Vocab card structure, Concept card structure, Dual file output, Chat quiz mode (opt-in), Canonical skeleton — review file (...), Short rendered example — drill file (...), Failure modes. The actual count depends on how the optional subheading "Failure modes" interacts; if grep shows 13, that's also acceptable.

- [ ] **Step 4: Commit**

```bash
cd /Users/priyeshpatel/Skills/ascii-canvas && \
  git add formats/flashcards.md && \
  git commit -m "feat(flashcards): add flashcards format spec file"
```

---

# Phase 3 — The example file

## Task 5: Write examples/flashcards-example.md

**Files:**
- Create: `/Users/priyeshpatel/Skills/ascii-canvas/examples/flashcards-example.md`

- [ ] **Step 1: Author the file with the full content below**

Write a 10-card mixed deck (5 vocab + 5 concept) on Spanish verbs:

````markdown
# flashcards — full example

**Topic:** Spanish verbs — 10 mixed cards (5 vocab + 5 concept)
**Width budget:** 80 cols
**Mode:** Unicode (the drill divider `╞═╡` is Unicode-only — flashcards doesn't have an ASCII fallback)
**Files:** `<slug>.md` (review, shown below) + `<slug>-drill.md` (auto-generated, fronts only — not shown here for brevity)

---

# Spanish verbs — top 10

10-card deck covering the most common Spanish verbs and the patterns that
beginners stumble on most.

---

```
┌─ Card 1 ──────────────────────────────────────────────────────────────────────┐
│                                                                                │
│             ser                                                                │
│             v.                                                                 │
│                                                                                │
╞════════════════════════════════════════════════════════════════════════════════╡
│                                                                                │
│   Meaning:   to be (identity, essence, permanence)                             │
│   Example:   Soy Carlos.                                                       │
│               I am Carlos.                                                     │
│   Hook:      ser = WHO you are                                                 │
│                                                                                │
└────────────────────────────────────────────────────────────────────────────────┘

┌─ Card 2 ──────────────────────────────────────────────────────────────────────┐
│                                                                                │
│             estar                                                              │
│             v.                                                                 │
│                                                                                │
╞════════════════════════════════════════════════════════════════════════════════╡
│                                                                                │
│   Meaning:   to be (state, mood, location, temporary)                          │
│   Example:   Estoy cansado.                                                    │
│               I am tired.                                                      │
│   Hook:      estar = HOW you are                                               │
│                                                                                │
└────────────────────────────────────────────────────────────────────────────────┘

┌─ Card 3 ──────────────────────────────────────────────────────────────────────┐
│                                                                                │
│             tener                                                              │
│             v.                                                                 │
│                                                                                │
╞════════════════════════════════════════════════════════════════════════════════╡
│                                                                                │
│   Meaning:   to have                                                           │
│   Example:   Tengo treinta años.                                               │
│               I am thirty (years old).                                         │
│   Hook:      Spanish "has" age; English "is" age                               │
│                                                                                │
└────────────────────────────────────────────────────────────────────────────────┘

┌─ Card 4 ──────────────────────────────────────────────────────────────────────┐
│                                                                                │
│             hacer                                                              │
│             v.                                                                 │
│                                                                                │
╞════════════════════════════════════════════════════════════════════════════════╡
│                                                                                │
│   Meaning:   to do, to make                                                    │
│   Example:   ¿Qué haces?                                                       │
│               What are you doing?                                              │
│   Hook:      "hacer" handles both "do" and "make" in Spanish                   │
│                                                                                │
└────────────────────────────────────────────────────────────────────────────────┘

┌─ Card 5 ──────────────────────────────────────────────────────────────────────┐
│                                                                                │
│             gustar                                                             │
│             v.                                                                 │
│                                                                                │
╞════════════════════════════════════════════════════════════════════════════════╡
│                                                                                │
│   Meaning:   to be pleasing to (inverse of "to like")                          │
│   Example:   Me gusta el café.                                                 │
│               Coffee is pleasing to me (= I like coffee).                      │
│   Hook:      Subject and object are reversed from English                      │
│                                                                                │
└────────────────────────────────────────────────────────────────────────────────┘

┌─ Card 6 ──────────────────────────────────────────────────────────────────────┐
│                                                                                │
│   When to use ser vs estar?                                                    │
│                                                                                │
╞════════════════════════════════════════════════════════════════════════════════╡
│                                                                                │
│   ser  = identity / origin / permanent traits / time                           │
│   estar = location / mood / temporary state / ongoing action                   │
│   Example: Es aburrido (boring person) vs Está aburrido (bored now)            │
│   Pitfall: Don't use ser for "how I feel today" — that's estar                 │
│                                                                                │
└────────────────────────────────────────────────────────────────────────────────┘

┌─ Card 7 ──────────────────────────────────────────────────────────────────────┐
│                                                                                │
│   How do you say your age in Spanish?                                          │
│                                                                                │
╞════════════════════════════════════════════════════════════════════════════════╡
│                                                                                │
│   Use TENER, not SER. "Tengo 30 años" = I have 30 years.                       │
│   Example: ¿Cuántos años tienes? — Tengo veinticinco.                          │
│   Pitfall: "Soy 30 años" sounds bizarre to a native speaker                    │
│                                                                                │
└────────────────────────────────────────────────────────────────────────────────┘

┌─ Card 8 ──────────────────────────────────────────────────────────────────────┐
│                                                                                │
│   How does "gustar" work grammatically?                                        │
│                                                                                │
╞════════════════════════════════════════════════════════════════════════════════╡
│                                                                                │
│   gustar is INVERTED: the thing liked is the subject, the liker is object.     │
│   Me gusta X = X is pleasing to me. Plural: Me gustan los libros.              │
│   Pitfall: "Yo gusto el café" is wrong; the café likes you in that sentence.   │
│                                                                                │
└────────────────────────────────────────────────────────────────────────────────┘

┌─ Card 9 ──────────────────────────────────────────────────────────────────────┐
│                                                                                │
│   What's the difference between tú and usted?                                  │
│                                                                                │
╞════════════════════════════════════════════════════════════════════════════════╡
│                                                                                │
│   tú = informal "you" (friends, peers, kids)                                   │
│   usted = formal "you" (strangers, elders, business, professional contexts)    │
│   Example: ¿Cómo estás? (tú) vs ¿Cómo está? (usted)                            │
│   Pitfall: When unsure, default to usted; let them downgrade to tú             │
│                                                                                │
└────────────────────────────────────────────────────────────────────────────────┘

┌─ Card 10 ─────────────────────────────────────────────────────────────────────┐
│                                                                                │
│   What's the pattern for present-tense regular -ar verbs?                      │
│                                                                                │
╞════════════════════════════════════════════════════════════════════════════════╡
│                                                                                │
│   Stem + endings: -o / -as / -a / -amos / -an                                  │
│   Example: hablar (to speak) → hablo / hablas / habla / hablamos / hablan      │
│   Pitfall: -er and -ir verbs use different endings; don't mix patterns         │
│                                                                                │
└────────────────────────────────────────────────────────────────────────────────┘
```

---

## Why this works

- **Mixed subtypes interleaved naturally:** Cards 1-5 are vocab (term + meaning + example + hook), Cards 6-10 are concept (question + definition + example + pitfall). Same outer frame, different internal structure, all in one deck.
- **A10 deck arc:** 10 cards fits the 8-15 default. Each card earns its existence — no filler.
- **Memory hooks:** Card 1's "ser = WHO you are" pairs with Card 2's "estar = HOW you are" to make the contrast stick.
- **Pitfalls do real work:** Cards 6-9 each name the most common beginner mistake, which is exactly what the user will encounter in conversation. Bare definitions don't teach as well as "here's the trap."
- **Width-disciplined:** Every card frame is exactly 80 cols. Long example sentences (Card 3 "Tengo treinta años...") are kept short enough to fit on a single line. Card 8's "Me gusta X = X is pleasing to me" stays under width by using "X" instead of repeating the noun.

## ASCII variant

Flashcards does not ship an ASCII fallback. The drill divider `╞═══╡` uses heavy double box-drawing characters that have no clean ASCII equivalent preserving the visual "fold" between front and back. If a user explicitly requests plain-ASCII output, the skill falls back to `cheat-sheet` per the failure-mode in `flashcards.md` and the format-fallback map in `qa-checklist.md`.
````

- [ ] **Step 2: Verify width**

Run:
```bash
python3 -c "
import re
c = open('/Users/priyeshpatel/Skills/ascii-canvas/examples/flashcards-example.md').read()
blocks = re.findall(r'\`\`\`[a-z]*\n(.*?)\`\`\`', c, re.DOTALL)
for i, b in enumerate(blocks, 1):
    w = max(len(l) for l in b.split('\n')) if b.strip() else 0
    print(f'block {i}: width {w}/80')
"
```
Expected: every block ≤ 80.

- [ ] **Step 3: Commit**

```bash
cd /Users/priyeshpatel/Skills/ascii-canvas && \
  git add examples/flashcards-example.md && \
  git commit -m "feat(flashcards): add flashcards example artifact"
```

---

# Phase 4 — SKILL.md updates

## Task 6: Update SKILL.md — description, routing matrix, tie-breakers

**Files:**
- Modify: `SKILL.md`

- [ ] **Step 1: Update YAML description trigger examples**

Find the `description:` line in the frontmatter. Change:
```
... timeline, comic strip, etc.) OR asks for ...
```
to:
```
... timeline, comic strip, flashcards, etc.) OR asks for ...
```

- [ ] **Step 2: Update the "Fire on:" explicit examples**

Find the bullet starting `- Explicit format requests:`. Append these trigger phrases at the end of the existing list (after `"anthropomorphize X"`):

```
, "make flashcards", "flashcard deck", "vocab cards", "study cards", "Anki-style cards", "drill me on X", "quiz me on X", "test me on X", "help me memorize X"
```

- [ ] **Step 3: Add routing matrix rows**

Find the routing-matrix code block. Add these two rows at the bottom of the matrix (after the comic rows):

```
   recall / memorization drill       → flashcards
   quiz / test self                  → flashcards
```

- [ ] **Step 4: Add tie-breakers**

Find the existing tie-breakers section. Add these two lines after the comic tie-breakers and before the "Do NOT combine" line:

```
   - Flashcards vs cheat-sheet       → flashcards for active recall, cheat-sheet for passive reference
   - Flashcards vs comparison-table  → comparison-table for side-by-side, flashcards for sequential Q/A
```

- [ ] **Step 5: Verify**

Run:
```bash
grep -c "flashcards" /Users/priyeshpatel/Skills/ascii-canvas/SKILL.md
```
Expected: at least 5 (description + explicit triggers + 2 routing rows + 2 tie-breakers).

Run:
```bash
grep -c "recall / memorization drill" /Users/priyeshpatel/Skills/ascii-canvas/SKILL.md
```
Expected: `1`

- [ ] **Step 6: Commit**

```bash
cd /Users/priyeshpatel/Skills/ascii-canvas && \
  git add SKILL.md && \
  git commit -m "feat(flashcards): wire flashcards into SKILL.md routing + triggers"
```

---

# Phase 5 — Acceptance suite

## Task 7: Run 3 flashcards-specific prompts + 2 regression prompts

**Files:**
- Create: `/Users/priyeshpatel/Skills/ascii-canvas/docs/flashcards-acceptance-results.md`

- [ ] **Step 1: Run prompt F1 — vocab deck**

Prompt:

> Make me flashcards for the most common 12 Spanish verbs.

Expected structural checks:
- (a) routes to flashcards format (not cheat-sheet)
- (b) 12 vocab cards (matching user's explicit count via U5 override)
- (c) every card has `┌─ Card N ─` numbered 1..12
- (d) every card has the drill divider `╞════╡`
- (e) every card frame is exactly 80 cols wide
- (f) BOTH files saved: `<slug>.md` (review) AND `<slug>-drill.md` (drill, fronts only)
- (g) drill file has NO drill dividers and NO back content
- (h) post-save block is 3 lines (Saved to: + review + drill)
- (i) skill offers to quiz at end ("Want me to quiz you...?")

- [ ] **Step 2: Run prompt F2 — concept deck**

Prompt:

> Concept flashcards drilling Next.js hooks.

Expected:
- (a) routes to flashcards format
- (b) ~10 concept cards (default 8-15) — useState, useEffect, useMemo, useCallback, useRef, useContext, useReducer, useImperativeHandle, useLayoutEffect, useTransition
- (c) cards use concept structure (question/term front, definition + example + pitfall back)
- (d) ≤80 cols, drill divider present
- (e) BOTH files saved
- (f) drill file has fronts only

- [ ] **Step 3: Run prompt F3 — chat quiz mode**

Prompt (after F1 has been run and the Spanish verbs deck exists):

> Quiz me on the Spanish verbs I just made.

Expected:
- (a) skill reads existing deck from `~/Ascii-diagrams/2026-05/2026-05-18-spanish*.md` (does NOT regenerate)
- (b) enters quiz loop — shows Card 1 front, waits for answer
- (c) compares user's answer using generous-on-semantics, strict-on-conjugation rules
- (d) reveals back card-by-card after each answer
- (e) emits end-of-quiz summary with correct/wrong count + redrill list
- (f) NO state persisted to disk

- [ ] **Step 4: Run regression prompts R1 and R2**

**R1:** "Cheat sheet for git daily commands."

Expected: routes to **cheat-sheet** (NOT flashcards — user said "cheat sheet" explicitly). Single file (cheat-sheet, not dual). ≤95 cols.

**R2:** "Make me a comic teaching the ser vs estar mistake."

Expected: routes to **comic** (NOT flashcards). 3-5 panels with characters. v1.1.0 behavior unchanged.

- [ ] **Step 5: Document results**

Write to `/Users/priyeshpatel/Skills/ascii-canvas/docs/flashcards-acceptance-results.md`:

````markdown
# Flashcards format acceptance suite — 2026-05-18

## F1: Make me flashcards for the most common 12 Spanish verbs.

**Expected:** flashcards / 12 vocab cards / dual file save / quiz offered
**Observed:** <fill in>
**Structural checks:**
- (a) routes to flashcards: PASS/FAIL
- (b) 12 cards: PASS/FAIL
- (c) sequential Card N numbering: PASS/FAIL
- (d) drill divider on every card: PASS/FAIL
- (e) 80 cols exact: PASS/FAIL
- (f) both files saved: PASS/FAIL
- (g) drill file fronts only: PASS/FAIL
- (h) 3-line post-save block: PASS/FAIL
- (i) quiz offered: PASS/FAIL
**Verdict:** PASS / FAIL

## F2: Concept flashcards drilling Next.js hooks.
[same structure]

## F3: Quiz me on the Spanish verbs I just made.
[same structure]

## R1: Cheat sheet for git daily commands.
[same structure]

## R2: Make me a comic teaching the ser vs estar mistake.
[same structure]

## Summary

- Flashcards prompts (F1-F3): N/3 pass
- Regression prompts (R1-R2): N/2 pass
- Files created at ~/Ascii-diagrams/2026-05/: [list]
- Issues to address: [list or "none"]
````

- [ ] **Step 6: Fix any failures**

For each FAIL: identify which file caused it, fix with `fix:` commit, re-run failing prompt, update results doc. Iterate until 5/5 pass.

- [ ] **Step 7: Commit results**

```bash
cd /Users/priyeshpatel/Skills/ascii-canvas && \
  git add docs/flashcards-acceptance-results.md && \
  git commit -m "docs: record v1.2.0 flashcards format acceptance suite"
```

- [ ] **Step 8: Tag v1.2.0**

Only after 5/5 prompts pass:

```bash
cd /Users/priyeshpatel/Skills/ascii-canvas && \
  git tag -a v1.2.0 -m "ascii-canvas v1.2.0 — add flashcards format (18 formats, A10 deck arc, dual file output, opt-in chat quiz mode)"
```

---

# Done criteria

The implementation is v1.2.0-complete when:

1. All 7 tasks completed with focused commits
2. `git log --oneline` shows ~8 new commits since v1.1.0
3. All 5 acceptance prompts pass (3 flashcards-specific + 2 regression)
4. Strict QA catches: a deliberate malformed deck (e.g., card 3 missing drill divider) → fail-twice → simplify or reroute
5. Repository tagged `v1.2.0`
6. The `ascii-canvas` skill description in SKILL.md frontmatter mentions flashcards as a trigger keyword

---

# File summary

**New (2 files):**
- `formats/flashcards.md`
- `examples/flashcards-example.md`

**Modified (4 files):**
- `composition-rules/width-budgets.md`
- `composition-rules/narrative-arcs.md`
- `composition-rules/qa-checklist.md`
- `SKILL.md`

**Added in docs (1 file):**
- `docs/flashcards-acceptance-results.md`

**Already committed (1 file):**
- `docs/2026-05-18-flashcards-format-design.md` (the spec, committed before this plan)

**Total: 7 files touched, ~8 commits, 1 new tag.**
