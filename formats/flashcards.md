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
┌─ Card N ─────────────────────────────────────────────────────────────────────┐
│                                                                              │
│             <term>                                                           │
│             [optional: pronunciation guide]                                  │
│             [optional: part of speech — n. / v. / adj. / adv.]               │
│                                                                              │
╞══════════════════════════════════════════════════════════════════════════════╡
│                                                                              │
│   Meaning:   <translation / one-line definition>                             │
│   Example:   <example sentence in source language>                           │
│               <English gloss of the example>                                 │
│   Hook:      <mnemonic / memory hook>  [optional]                            │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

## Concept card structure

```
┌─ Card N ─────────────────────────────────────────────────────────────────────┐
│                                                                              │
│   <term or short question>                                                   │
│                                                                              │
╞══════════════════════════════════════════════════════════════════════════════╡
│                                                                              │
│   <definition — 1-3 lines>                                                   │
│   Example: <key example or analogy>  [optional]                              │
│   Pitfall: <common mistake>  [optional]                                      │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

## Dual file output

Flashcards always produces TWO files (auto-saved):

### Review file

Path: `~/Ascii-diagrams/YYYY-MM/YYYY-MM-DD-<slug>.md`

Full deck with folded layout (front + drill divider + back per card).

### Drill file

Path: `~/Ascii-diagrams/YYYY-MM/YYYY-MM-DD-<slug>-drill.md`

Same cards but back side removed. Cards in the drill file have a smaller frame — just front content, no drill divider, no back.

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
- **If user already has a deck file from a previous turn** and says "quiz me on the X I just made" — read the existing deck file from `~/Ascii-diagrams/` and start the quiz loop without regenerating

### If user says no

Skill responds with just the post-save block and ends the turn.

## Canonical skeleton — review file (3-card sample, 2 vocab + 1 concept)

```
# Spanish — top 3 verbs

3-card mixed deck covering ser, estar, and the ser-vs-estar contrast.

┌─ Card 1 ─────────────────────────────────────────────────────────────────────┐
│                                                                              │
│             ser                                                              │
│             v.                                                               │
│                                                                              │
╞══════════════════════════════════════════════════════════════════════════════╡
│                                                                              │
│   Meaning:   to be (identity, essence, permanence)                           │
│   Example:   Soy Carlos.                                                     │
│               I am Carlos.                                                   │
│   Hook:      ser = WHO you are                                               │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘

┌─ Card 2 ─────────────────────────────────────────────────────────────────────┐
│                                                                              │
│             estar                                                            │
│             v.                                                               │
│                                                                              │
╞══════════════════════════════════════════════════════════════════════════════╡
│                                                                              │
│   Meaning:   to be (state, mood, location, temporary)                        │
│   Example:   Estoy cansado.                                                  │
│               I am tired.                                                    │
│   Hook:      estar = HOW you are                                             │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘

┌─ Card 3 ─────────────────────────────────────────────────────────────────────┐
│                                                                              │
│   When to use ser vs estar?                                                  │
│                                                                              │
╞══════════════════════════════════════════════════════════════════════════════╡
│                                                                              │
│   ser = identity / origin / permanent traits / time                          │
│   estar = location / mood / temporary state / ongoing action                 │
│   Example:  Es aburrido (boring person) vs Está aburrido (bored now)         │
│   Pitfall:  Don't use ser for "how I feel today" — that's estar              │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

## Short rendered example — drill file (matching 3 cards, fronts only)

```
# Spanish — top 3 verbs — drill mode

3 cards. Try to recall each card's answer. Then open the review file to check.

┌─ Card 1 ─────────────────────────────────────────────────────────────────────┐
│                                                                              │
│             ser                                                              │
│             v.                                                               │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘

┌─ Card 2 ─────────────────────────────────────────────────────────────────────┐
│                                                                              │
│             estar                                                            │
│             v.                                                               │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘

┌─ Card 3 ─────────────────────────────────────────────────────────────────────┐
│                                                                              │
│   When to use ser vs estar?                                                  │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

## Failure modes

- If the topic has no discrete recall-able items → fall back to `cheat-sheet`
- If a card's back overflows 5 lines → split into two cards (e.g., card 5 "ser uses" splits into 5a "ser for identity" and 5b "ser for time/origin")
- If width overflows at 80 cols → shorten term, abbreviate meaning, or drop optional fields (pronunciation, hook)
- If user requests >30 cards in one deck → split into themed sub-decks; offer "I'll make 3 separate decks"
- If the same term appears twice → consolidate or split into different facets (one card per facet)
- If user wants spaced-repetition tracking → out of scope in v1.2; suggest manual rotation through the drill file or external tool (Anki)
