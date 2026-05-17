# comic

## Purpose

Compose ASCII comic strips with stick-figure-body characters, emoticon-face moods, speech bubbles, and narration boxes — to teach concepts through dialogue, demonstrate wrong/right patterns, or anthropomorphize technical concepts.

## Use when

- Teaching a language concept through dialogue and character moments ("ser vs estar")
- Demonstrating a wrong-then-right pattern with two characters
- Anthropomorphizing a technical concept (Webhook walks into a Door, OAuth as two people at a bar)
- Making an explainer "engaging" through characters rather than abstract slides
- The topic has natural characters or could be illustrated as a skit

## Do NOT use when

- The topic is purely abstract with no characters and nothing to anthropomorphize → use `slideshow`
- The topic is technical actors with named API messages → use `sequence-diagram`
- The user explicitly asks for plain-ASCII output (comic relies on Unicode emoticons + box-drawing) → fall back to `slideshow`
- The topic is a linear how-to with no characters → use `step-by-step-guide`

## Width budget

100 cols

## Arc

A9 — Comic arc family (4 variants). See `composition-rules/narrative-arcs.md`.

- **A9.1 Teaching** (3–5 panels, default 4) — language lessons, wrong-then-right
- **A9.2 Contrast** (2 panels exactly) — binary ❌/✓ rules
- **A9.3 Joke** (2–3 panels, default 3) — one-liners with punchline
- **A9.4 Tech-explainer** (4 panels) — anthropomorphized concepts with narration

The format file's routing logic picks the variant based on the user's prompt; the four arcs share grammar.

## Layout rules

- **Vertical strip** — panels stacked top-to-bottom, one per row. Single column.
- **Panel frame** uses light box-drawing `┌─┐│└─┘` consistent with the rest of the skill (box-drawing.md R3).
- **Panel title** at top-left of frame: `┌── Panel N: <optional title> ──`. Optional but recommended.
- **Panels separated by `\n\n`** (one blank line). No `---` divider between panels — the panel frames themselves provide separation.
- **Character glyph** is a 4-line vertical stack: optional name label, face, neck `│`, arms `╱│╲`, legs `╱ ╲`.
- **Bracket-shape grammar:** `(...)` female, `[...]` male, `{...}` non-binary/neutral, `<...>` anthropomorphized concept.
- **Speech bubble grammar (hybrid):**
  - Short dialogue (≤50 chars): inline tail `── "..."`
  - Long or multi-line dialogue: boxed bubble `╭──...──╮ │ ... │ ╰──...──╯` with `──` connector
  - Thought: dotted tail `··· "..."`
  - Narration box: `┌── narración ──┐ ... └────...────┘` at top or bottom of panel
- **Two-character panels:** left character has `(face) ── "text"`, right character has `"text" ── (face)` — tail mirrors the speaker's position.
- **Max 3 characters per panel** (per scope cut).

## Face library (15 moods)

Wrap the inner expression in the character's bracket type to render.

| Mood | Inner | Mood | Inner | Mood | Inner |
|---|---|---|---|---|---|
| happy | `•‿•` | surprised | `O_o` | confused | `•_•?` |
| skeptical | `¬_¬` | smug | `¬‿¬` | sad | `T_T` |
| flat | `-_-` | excited | `★_★` | mortified | `×_×` |
| thinking | `‒.‒` | dawning | `•◡•` | delighted | `^_^` |
| embarrassed | `>_<` | sleepy | `˘_˘` | determined | `•̀_•́` |

Custom faces allowed: 3–4 cols inside the bracket, convention `<eye><mouth><eye>` (plus optional 1-char mood marker like the `?` in `•_•?`).

## Canonical skeleton — Unicode (A9.1 Teaching arc, 4 panels)

```
┌── Panel 1: Setup ────────────────────────────────────────────────────────────────────────────┐
│                                                                                               │
│   <Char A>                                                                                    │
│   (<confident face>) ── "<line where the wrong approach is taken>"                            │
│      │                                                                                        │
│     ╱│╲                                                                                       │
│     ╱ ╲                                                                                       │
│                                                                                               │
└───────────────────────────────────────────────────────────────────────────────────────────────┘

┌── Panel 2: Confusion ────────────────────────────────────────────────────────────────────────┐
│                                                                                               │
│   <Char A>                                            <Char B>                                │
│   (<same face>) ── "<same wrong line>"                       "...¿qué?" ── (<skeptical>)      │
│      │                                                          │                             │
│     ╱│╲                                                        ╱│╲                            │
│     ╱ ╲                                                        ╱ ╲                            │
│                                                                                               │
└───────────────────────────────────────────────────────────────────────────────────────────────┘

┌── Panel 3: Reveal ───────────────────────────────────────────────────────────────────────────┐
│                                                                                               │
│   <Char A>                                            <Char B>                                │
│   (<dawning>) ── "<the correct rule>"                        "<correction>" ── (<delighted>)  │
│      │                                                          │                             │
│     ╱│╲                                                        ╱│╲                            │
│     ╱ ╲                                                        ╱ ╲                            │
│                                                                                               │
└───────────────────────────────────────────────────────────────────────────────────────────────┘

┌── Panel 4: Application ──────────────────────────────────────────────────────────────────────┐
│                                                                                               │
│   <Char A>                                                                                    │
│   (<happy>) ── "<the corrected line>"                                                         │
│      │                                                                                        │
│     ╱│╲                                                                                       │
│     ╱ ╲                                                                                       │
│                                                                                               │
└───────────────────────────────────────────────────────────────────────────────────────────────┘
```

## Short rendered example (A9.2 Contrast arc, 2 panels)

A canonical "ser vs estar" contrast — wrong panel, then right panel.

```
┌── ❌ Panel 1: Wrong way ─────────────────────────────────────────────────────────────────────┐
│                                                                                               │
│   Priyesh                                                                                     │
│   (•_•) ── "Yo soy 30 años."                                                                  │
│     │                                                                                         │
│    ╱│╲                                                                                        │
│    ╱ ╲                                                                                        │
│                                                                                               │
│   ┌── narración ───────────────────────────────────────────────────────────────────────────┐ │
│   │  "Yo soy 30 años" literally means "I AM 30 years" — using ser. Wrong verb.              │ │
│   └─────────────────────────────────────────────────────────────────────────────────────────┘ │
│                                                                                               │
└───────────────────────────────────────────────────────────────────────────────────────────────┘

┌── ✓ Panel 2: Right way ──────────────────────────────────────────────────────────────────────┐
│                                                                                               │
│   Priyesh                                                                                     │
│   (•◡•) ── "Tengo 30 años."                                                                   │
│     │                                                                                         │
│    ╱│╲                                                                                        │
│    ╱ ╲                                                                                        │
│                                                                                               │
│   ┌── narración ───────────────────────────────────────────────────────────────────────────┐ │
│   │  "Tengo 30 años" = "I HAVE 30 years" — tener for age. Always.                           │ │
│   └─────────────────────────────────────────────────────────────────────────────────────────┘ │
│                                                                                               │
└───────────────────────────────────────────────────────────────────────────────────────────────┘
```

## Failure modes

- If user explicitly requests ASCII fallback → fall back to `slideshow` (comic depends on Unicode emoticons + rounded bubble corners that have no clean ASCII equivalents)
- If the topic has no characters and no concept to anthropomorphize → fall back to `slideshow`
- If a panel needs more than 3 characters → split into more panels or use a narration box for context
- If dialogue won't fit at 100 cols → switch the line to a boxed bubble (gains vertical room) or move context to a narration box
- If the same character has the same face in every panel → fail strict QA item 5 → simplify or reroute to slideshow per `qa-checklist.md`
- If the user wants more than 8 panels without explicit request → compress; offer to split into a sequel comic
- If the joke isn't landing in an A9.3 (subjective — skill can't detect) → ship anyway; let user iterate
