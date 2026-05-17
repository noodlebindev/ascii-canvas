# Comic format — Design Spec (v1.1.0)

**Date:** 2026-05-18
**Status:** Spec — ready for implementation plan
**Skill version bump:** v1.0.0 → v1.1.0 (additive — no breaking changes)
**Spec location:** `~/Skills/ascii-canvas/docs/2026-05-18-comic-format-design.md`

---

## 1. Purpose

Add `comic` as the 17th format in the ascii-canvas catalog. Compose ASCII comic strips — characters with stick-figure bodies, emoticon faces, speech bubbles, and narration boxes — for two primary use cases:

1. **Language / dialogue learning** — teach grammar and idioms through wrong-then-right character moments.
2. **Educational / explainer comics** — teach technical concepts by anthropomorphizing them (HTTP, webhooks, OAuth, type systems, etc.).

The skill is a guide. Authoring stays Claude-only. No external dependencies. No code.

## 2. Scope

**In scope (v1.1.0):**
- New format file: `formats/comic.md`
- New example file: `examples/comic-example.md`
- New arc family: A9 with 4 variants (teaching, contrast, joke, tech-explainer) added to `composition-rules/narrative-arcs.md`
- New width-budget entry: `comic` → 100 cols in `composition-rules/width-budgets.md`
- SKILL.md description + routing matrix updates
- QA additions specific to comic in `composition-rules/qa-checklist.md`
- Version tag bump to `v1.1.0`

**Out of scope (deferred to future):**
- Sound effects (`POW!` `BAM!`)
- Motion lines, action arrows, speed marks
- Backgrounds / scenery (setting conveyed via narration box or panel title)
- 4+ characters in a single panel
- Color / ANSI escapes (excluded at skill level)
- Animated / multi-state characters within a single panel
- Comic-combination outputs (slideshow with embedded comic panels)

## 3. Architecture

**File additions:**
```
~/Skills/ascii-canvas/
├── formats/
│   └── comic.md               ← NEW
├── composition-rules/
│   ├── narrative-arcs.md      ← UPDATE: add A9 family with 4 variants
│   ├── width-budgets.md       ← UPDATE: add comic = 100 cols
│   └── qa-checklist.md        ← UPDATE: add comic-specific QA points + fallback entry
├── examples/
│   └── comic-example.md       ← NEW
├── SKILL.md                   ← UPDATE: trigger keywords + routing matrix
└── docs/
    └── 2026-05-18-comic-format-design.md   ← this spec
```

**No file removals. No restructures.** All changes are additive.

**Format catalog count:** 16 → 17.

## 4. Character glyph grammar

Every character occupies a vertical 4-line stack (name label optional):

```
   Sofía            Carlos             Webhook            (unnamed)
   (•‿•)            [•_•]              <•_•>              (•‿•)
     │                │                  │                  │
    ╱│╲              ╱│╲                ╱│╲                ╱│╲
    ╱ ╲              ╱ ╲                ╱ ╲                ╱ ╲
```

### 4.1 Bracket-shape grammar (carries identity class)

| Bracket | Meaning | When to use |
|---|---|---|
| `(...)` | Female | Default for female characters |
| `[...]` | Male | Default for male characters |
| `{...}` | Non-binary / neutral | When gender shouldn't be marked |
| `<...>` | Anthropomorphized concept | Tech-explainer: `<Webhook>`, `<Bug>`, `<OAuth>`, `<HTTPRequest>` |

### 4.2 Name label rules

- Plain text above the face (no brackets — to avoid visual clash with the `[face]` bracket).
- Centered above the character glyph.
- Omit if only one character in the comic AND character is unnamed.
- Required in multi-character scenes (≥2 characters in any panel).
- Must be consistent across panels — the same character keeps the same bracket type and label everywhere.

### 4.3 Body grammar

Same for all characters regardless of bracket choice:
```
   │     (neck)
  ╱│╲    (torso + arms)
  ╱ ╲    (legs)
```

Body posture is consistent — no gendered body variations. Identity is carried by bracket + label + face mood.

## 5. Face library (15 moods)

Listed as inner expressions; wrap in the character's bracket type to render.

| Mood | Inner | Mood | Inner | Mood | Inner |
|---|---|---|---|---|---|
| happy | `•‿•` | surprised | `O_o` | confused | `•_•?` |
| skeptical | `¬_¬` | smug | `¬‿¬` | sad | `T_T` |
| flat | `-_-` | excited | `★_★` | mortified | `×_×` |
| thinking | `‒.‒` | dawning | `•◡•` | delighted | `^_^` |
| embarrassed | `>_<` | sleepy | `˘_˘` | determined | `•̀_•́` |

**Custom faces are allowed** — authors can invent new moods following the convention `<eye><mouth><eye>` plus optional 1-char mood marker (the `?` in `•_•?` for confused). The inner expression must be 3-4 cols wide so the full glyph (bracket + face + bracket) stays at 5-6 cols and doesn't break panel alignment.

## 6. Speech bubble grammar (hybrid)

### 6.1 Short inline dialogue (≤ 50 chars)

```
   (•‿•) ── "¡Hola! ¿Cómo te llamas?"
```

Tail `──` from face glyph to opening quote. Quotes always doubled `"`. Punctuation inside quotes per language convention (Spanish: `¡` `¿`).

### 6.2 Boxed bubble (> 50 chars OR multi-line)

```
   (•‿•) ── ╭──────────────────────────────────────────╮
              │ I had to write three paragraphs of      │
              │ confusing prose to demonstrate this.    │
              ╰──────────────────────────────────────────╯
```

Bubble corners use `╭╮╰╯` (rounded). Vertical sides use `│`. Connector tail `──` from character face to bubble's left edge.

### 6.3 Thought bubble (internal monologue)

```
   (•_•?) ··· "wait, do I use ser or estar here?"
```

Tail uses dots `···` instead of dashes. Indicates internal monologue or unspoken thought.

### 6.4 Narration box (no speaker)

```
┌── narración ────────────────────────────────────────────────────────────┐
│  When a webhook arrives at the platform, it must first prove its         │
│  identity before any action is taken.                                    │
└──────────────────────────────────────────────────────────────────────────┘
```

- Full panel width (panel inner content area minus 1 col padding each side).
- Top-left label `── narración ──` (or `── narration ──` in English) gives semantic frame.
- Used for setting/scene context, abstract introductions, takeaways.
- Maximum **one narration box per panel** (top OR bottom, not both) — unless the panel is in A9.4 tech-explainer arc with explicit framing + takeaway pair.

## 7. Panel structure

```
┌── Panel N: <optional scene/title> ──────────────────────────────────────┐
│                                                                          │
│   [optional narration box at top]                                        │
│                                                                          │
│   <Character A glyph>  ── "dialogue"                                     │
│                                                                          │
│                              "reply" ──  <Character B glyph>             │
│                                                                          │
│   [optional narration box at bottom]                                     │
│                                                                          │
└──────────────────────────────────────────────────────────────────────────┘
```

- Panel frame uses light box-drawing `┌─┐│└─┘` (consistent with rest of skill per box-drawing.md R3).
- Panel title at top-left: `┌── Panel N: <title> ──` — optional but recommended for setting context.
- Panels separated by `\n\n` (one blank line). **No `---` divider** between panels (would visually fight the panel frames).
- Single-character panels: character glyph centered or left-aligned at author's discretion.
- Two-character panels: speaker A on left, speaker B on right. Dialogue tail direction mirrors the speaker's position — left character's tail reads `(face) ── "text"`, right character's reads `"text" ── (face)`:
  ```
     (•‿•) ── "¡Hola!"
                                                "¡Hola, qué tal?" ── [•_•]
  ```

## 8. Width budget

**100 cols** — added to `composition-rules/width-budgets.md`.

Standard overflow rules:
1. Shorten dialogue
2. Move long dialogue to a boxed bubble (gains vertical room, keeps width)
3. Move context to a narration box
4. Split into more panels
5. Never widen past 100

## 9. Narrative arcs — A9 family

Added to `composition-rules/narrative-arcs.md` after A8.

### A9.1 — Teaching arc (3-5 panels, default 4)

1. **Setup** — character in normal state, doing the thing they think is correct
2. **Confusion / mistake** — character makes the common error; second character or narration reacts
3. **Reveal / correction** — the rule lands via the other character or a narration box
4. **Application (optional)** — character tries again, gets it right, *aha* face

**Use for:** language-learning lessons, common-mistake patterns, any wrong-then-right teachable beat.

### A9.2 — Contrast arc (exactly 2 panels)

1. **❌ Wrong way** — character demonstrates wrong approach; reaction face `(×_×)` or `(¬_¬)`
2. **✓ Right way** — character demonstrates right approach; reaction face `(•◡•)` or `(^_^)`

**Use for:** binary syntactic rules (ser vs estar, tú vs usted, `var` vs `let`). Maximum density: one panel per option, no exposition.

### A9.3 — Joke arc (2-3 panels, default 3)

1. **Setup** — character in mundane situation
2. **Twist** — something unexpected happens / character realizes
3. **Reaction (optional)** — beat panel, just a face, no dialogue

**Use for:** one-liners where the *point* is the joke. The reaction-only panel is the comic equivalent of a comedian's pause.

### A9.4 — Tech-explainer arc (4 panels, occasionally 3)

1. **Narration sets the stage** — `┌── narración ──┐` at top + anthropomorphized concept character introduced (uses `<...>` bracket)
2. **Approach** — concept attempts to do its job; encounters a gate / check / boundary
3. **Complication** — gate rejects, asks for proof, or creates friction (narration optional)
4. **Resolution** — concept presents the right credential; gate opens. Optional final narration with the takeaway rule.

**Use for:** APIs, protocols, system mechanics, abstract concepts that get easier with an avatar (HTTP, webhooks, race conditions, type systems, garbage collection).

### A9 — Universal panel rules (inherits from existing U1–U6 in narrative-arcs.md)

- Each panel must earn its existence
- Face moods must change panel-to-panel (static-face comic fails strict QA per §11)
- Default count per arc as stated above
- Never exceed 8 panels in any comic without explicit user request
- User override always wins ("make a 6-panel comic about X")

## 10. SKILL.md updates

### 10.1 Description / trigger keywords

Add to the SKILL.md frontmatter `description` field, appended to existing trigger examples:

> Explicit format requests: …, "make a comic", "comic strip", "comic-style", "as a skit", "as a scenario", "with characters", "dialogue between X and Y", "anthropomorphize X", "X walks into a Y".

### 10.2 Routing matrix additions

Add two new rows under "CHOOSE FORMAT" section in SKILL.md:
```
characters + dialogue + lesson      → comic
anthropomorphized concept           → comic
```

### 10.3 Tie-breaker additions (after existing tie-breakers)

- Comic vs slideshow ambiguous → **slideshow** (simpler — preserves existing tie-break rule)
- Comic vs sequence-diagram ambiguous → comic for educational/narrative, sequence-diagram for technical/protocol
- Explicit comic keyword wins over inferred format (existing rule, no change)

## 11. QA additions

In `composition-rules/qa-checklist.md`, add a new subsection "Comic-specific strict QA" after the cross-artifact consistency check. Comic artifacts run the standard 8-point checklist PLUS these:

1. **Speaker identifiable** — every speech bubble has a `──` tail or connector that traces to a character glyph
2. **Character bracket consistency** — the same named character uses the same bracket type (round/square/curly/angle) across every panel
3. **At most one narration box per panel** — exception: A9.4 tech-explainer arc may have framing narration (top) + takeaway narration (bottom)
4. **≤3 characters per panel** — per scope cut
5. **Face mood varies across panels** — when the same character appears in multiple panels, their face must change at least once (static-face comic = lifeless comic = fail-twice triggers reroute to slideshow)
6. **Panel widths identical** — every panel frame is the same outer width (100 cols by default)

### 11.1 Format fallback addition

Add to the fallback map in `qa-checklist.md`:
```
| comic | slideshow |
```

Reason: if a comic can't be made coherent (e.g., no characters, no dialogue, no concept to anthropomorphize), the format falls back to slideshow as the next-simplest narrative explainer.

## 12. Save behavior

**Multi-panel comic (≥2 panels)** → auto-save to `~/Ascii-diagrams/YYYY-MM/YYYY-MM-DD-<slug>.md`.

**Single-panel captioned scene** → chat only.

No new save logic — comic inherits the existing rule "any artifact with more than one section" maps to auto-save.

## 13. Example file content

`examples/comic-example.md` ships with a richer reference artifact. Suggested topic:

**Topic:** Ser vs Estar — the classic "Yo soy 30 años" mistake (A9.1 teaching arc, 4 panels). Uses two named characters (Sofía female, Carlos male), demonstrates: setup → mistake → correction by Sofía → application by Carlos. Width 100, Unicode default.

Format file's inline example will be smaller (2-3 panels) showing one A9.2 contrast arc.

## 14. Build sequence (for the implementation plan)

1. Update `composition-rules/narrative-arcs.md` with A9 family
2. Update `composition-rules/width-budgets.md` with `comic = 100`
3. Update `composition-rules/qa-checklist.md` with comic-specific QA + fallback entry
4. Write `formats/comic.md` (full format file)
5. Write `examples/comic-example.md` (richer reference)
6. Update `SKILL.md` (description + routing matrix + tie-breakers)
7. Run acceptance suite: 3 comic-specific prompts + spot-check that existing 7 prompts still pass
8. Tag `v1.1.0`

## 15. Acceptance criteria

The format is v1.1.0-complete when:

1. All 6 files (1 new format, 1 new example, 3 updated composition-rules, 1 updated SKILL.md) committed and pushed to the skill's git repo
2. Existing 7-prompt acceptance suite from v1.0.0 still passes unchanged
3. Three new comic-specific acceptance prompts pass:
   - **C1:** "Make me a comic teaching the ser vs estar mistake." → A9.1 teaching arc, 3-5 panels, 2 characters, auto-saves
   - **C2:** "Comic-style ❌/✓ on tú vs usted." → A9.2 contrast arc, exactly 2 panels, auto-saves
   - **C3:** "Anthropomorphize Stripe webhook signature verification as a comic." → A9.4 tech-explainer, 4 panels with narration, `<Webhook>` character with angle brackets, auto-saves
4. Strict QA catches: a deliberate static-face comic (every panel same expression) → fail-twice → reroute to slideshow
5. Repository tagged `v1.1.0` after all checks pass

## 16. Out of scope — explicit non-goals

(Restated for clarity; the build must NOT include any of these.)

- Sound effects (`POW!` `BAM!`)
- Motion lines / action arrows
- Backgrounds / drawn scenery
- 4+ characters in a single panel
- Color / ANSI
- Animated / multi-state characters
- Comic embedded inside other formats
- Comic strips that exceed 8 panels without explicit user request

## 17. Open items

None. All design decisions resolved during brainstorming Q1–Q8.
