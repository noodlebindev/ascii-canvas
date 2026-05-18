# Comic Format (v1.1.0) Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add `comic` as the 17th format in the ascii-canvas skill, with stick-figure-body characters, emoticon-face moods, hybrid speech bubbles, narration boxes, 4 arc variants (teaching/contrast/joke/tech-explainer), and full routing/QA/save integration. Bump v1.0.0 → v1.1.0.

**Architecture:** Additive only. Three composition-rules files get updates, two new files are created (`formats/comic.md`, `examples/comic-example.md`), SKILL.md gets routing matrix + trigger keyword updates. No breaking changes to existing 16 formats.

**Tech Stack:** Markdown only. Git for version control. No build step. No external dependencies.

**Spec reference:** `docs/2026-05-18-comic-format-design.md`

**Verification model:** 3 comic-specific acceptance prompts + spot-check 3 existing prompts (to ensure no regressions) at the end. No per-task tests — format files are content, not code.

---

## Conventions used in this plan

- All paths absolute under ``.
- Every task ends with a `feat:`, `docs:`, or `chore:` commit.
- For each file, the FULL CONTENT to add is shown verbatim in the task step. No "similar to task N" references.
- "Verify" steps re-read the file or run a width-check command before committing.

---

# Phase 1 — Composition rules updates (foundation; comic depends on these)

## Task 1: Add comic width budget to width-budgets.md

**Files:**
- Modify: `composition-rules/width-budgets.md`

- [ ] **Step 1: Read the current file**

Run: open `composition-rules/width-budgets.md` and locate the `## Per-format budgets` table.

- [ ] **Step 2: Insert the comic row in the table**

The table is currently sorted by ascending width. Insert `comic` at the position where it fits (100 cols, alongside flowchart/timeline/mind-map/etc.). Add this row right after the `concept-stack` entry:

```markdown
| comic | 100 |
```

If alphabetical ordering is preferred, the row goes between `cheat-sheet` and `comparison-table` — either ordering is acceptable as long as the row is present.

- [ ] **Step 3: Verify**

Run:
```bash
grep -c "^| comic" composition-rules/width-budgets.md
```
Expected: `1`

- [ ] **Step 4: Commit**

```bash
cd ~/.claude/skills/ascii-canvas && \
  git add composition-rules/width-budgets.md && \
  git commit -m "feat(comic): add 100-col width budget"
```

---

## Task 2: Add A9 arc family to narrative-arcs.md

**Files:**
- Modify: `composition-rules/narrative-arcs.md`

- [ ] **Step 1: Locate the insertion point**

The file currently has arcs A1–A8 followed by `## Universal panel rules`. Insert the new A9 family BETWEEN `### A8 — Step-by-step-guide arc (4–7 steps)` and `## Universal panel rules (apply to every arc)`.

- [ ] **Step 2: Insert the A9 family content verbatim**

Add this exact content after the closing `**Use for:** simple processes (lighter than playbook).` line of A8 and before the `## Universal panel rules` heading:

````markdown
### A9 — Comic arc family (multi-variant)

The comic format ships with four named arc variants. The variant is chosen based on what the user is asking for; the format file's routing logic picks one. All four share the same panel/character/bubble grammar — they differ only in panel sequence and count.

#### A9.1 — Teaching arc (3–5 panels, default 4)

1. **Setup** — character in normal state, doing the thing they think is correct
2. **Confusion / mistake** — character makes the common error; second character or narration reacts
3. **Reveal / correction** — the rule lands via the other character or a narration box
4. **Application** *(optional)* — character tries again, gets it right, *aha* face

**Use for:** language-learning lessons, common-mistake patterns, any wrong-then-right teachable beat.

#### A9.2 — Contrast arc (exactly 2 panels)

1. **❌ Wrong way** — character demonstrates wrong approach; reaction face `(×_×)` or `(¬_¬)`
2. **✓ Right way** — character demonstrates right approach; reaction face `(•◡•)` or `(^_^)`

**Use for:** binary syntactic rules (ser vs estar, tú vs usted, `var` vs `let`). Maximum density.

#### A9.3 — Joke arc (2–3 panels, default 3)

1. **Setup** — character in mundane situation
2. **Twist** — something unexpected happens / character realizes
3. **Reaction** *(optional)* — beat panel, just a face, no dialogue

**Use for:** one-liners where the *point* is the joke.

#### A9.4 — Tech-explainer arc (4 panels, occasionally 3)

1. **Narration sets the stage** — `┌── narración ──┐` at top + anthropomorphized concept character introduced (uses `<...>` bracket)
2. **Approach** — concept attempts its job; encounters a gate / check / boundary
3. **Complication** — gate rejects or creates friction (narration optional)
4. **Resolution** — concept presents the right credential; gate opens. Optional final narration with takeaway rule.

**Use for:** APIs, protocols, system mechanics, abstract concepts that get easier with an avatar.

#### A9 — Comic-specific panel rules

In addition to universal rules U1–U6 below:
- **Face moods must change** when the same character appears in ≥2 panels (static-face comic = lifeless comic = strict QA failure → reroute to slideshow)
- **Default panel count per variant** as listed above; never exceed 8 without explicit user request
- **Compress before expanding** (U3 applies); drop optional panels (Application, Reaction) when the topic doesn't justify them
````

- [ ] **Step 3: Verify**

Run:
```bash
grep -c "^### A9\." composition-rules/narrative-arcs.md
```
Expected: `4` (one for each of A9.1, A9.2, A9.3, A9.4)

Also confirm:
```bash
grep -c "^## Universal panel rules" composition-rules/narrative-arcs.md
```
Expected: `1` (the existing universal-rules heading still present after the A9 insertion)

- [ ] **Step 4: Commit**

```bash
cd ~/.claude/skills/ascii-canvas && \
  git add composition-rules/narrative-arcs.md && \
  git commit -m "feat(comic): add A9 arc family with 4 variants"
```

---

## Task 3: Add comic-specific QA checks + fallback entry to qa-checklist.md

**Files:**
- Modify: `composition-rules/qa-checklist.md`

- [ ] **Step 1: Locate the Cross-artifact consistency check section**

In the file, find the heading `## Cross-artifact consistency check (in addition to the 8 points)`. The new comic-specific subsection inserts AFTER the end of that section's bullet list and BEFORE the `## When QA runs` heading.

- [ ] **Step 2: Insert the comic-specific QA subsection**

Add this content verbatim:

````markdown
## Comic-specific strict QA (in addition to the 8 points + cross-artifact check)

When the artifact is a comic, strict QA additionally verifies:

1. **Speaker identifiable** — every speech bubble has a `──` tail or connector that traces to a character glyph
2. **Character bracket consistency** — the same named character uses the same bracket type (`(...)` round / `[...]` square / `{...}` curly / `<...>` angle) across every panel
3. **At most one narration box per panel** — exception: A9.4 tech-explainer arc may have framing narration (top) + takeaway narration (bottom)
4. **≤3 characters per panel** — per scope cut in the design spec
5. **Face mood varies across panels** — when the same character appears in multiple panels, their face must change at least once (static-face comic = fail-twice triggers reroute to slideshow)
6. **Panel frame widths identical** — every panel's outer frame is the same width (100 cols by default)

````

- [ ] **Step 3: Add comic → slideshow to the fallback map**

Find the `## Format fallback map (graceful degradation)` table. Add this row at the bottom of the table (after the existing `decision-tree | comparison-table` row):

```markdown
| comic | slideshow |
```

- [ ] **Step 4: Verify**

Run:
```bash
grep -c "^## Comic-specific strict QA" composition-rules/qa-checklist.md
```
Expected: `1`

Run:
```bash
grep -c "^| comic | slideshow |" composition-rules/qa-checklist.md
```
Expected: `1`

- [ ] **Step 5: Commit**

```bash
cd ~/.claude/skills/ascii-canvas && \
  git add composition-rules/qa-checklist.md && \
  git commit -m "feat(comic): add comic-specific strict QA + slideshow fallback"
```

---

# Phase 2 — The format file

## Task 4: Write formats/comic.md

**Files:**
- Create: `formats/comic.md`

- [ ] **Step 1: Author the file with the full content below**

The format file must include the full template sections (Purpose, Use when, Do NOT use when, Width budget, Arc, Layout rules, Canonical skeleton — Unicode, Short rendered example, Failure modes) per the Task 7 template from the v1.0.0 plan. Comic has no ASCII fallback skeleton — the Unicode characters used (box-drawing + emoticons + `╭╮╰╯`) don't have clean pure-ASCII equivalents that preserve the comic feel; if a user explicitly requests ASCII, the format file's failure-mode section directs them to fall back to slideshow instead.

Full content to write:

````markdown
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
┌── Panel 1: Setup ───────────────────────────────────────────────────────────────────────────────┐
│                                                                                                  │
│   <Char A name>                                                                                  │
│   (<face: confident>) ── "<line where the wrong approach is taken>"                              │
│      │                                                                                           │
│     ╱│╲                                                                                          │
│     ╱ ╲                                                                                          │
│                                                                                                  │
└──────────────────────────────────────────────────────────────────────────────────────────────────┘

┌── Panel 2: Confusion ───────────────────────────────────────────────────────────────────────────┐
│                                                                                                  │
│   <Char A name>                                       <Char B name>                              │
│   (<face: same as Panel 1>) ── "<same wrong line>"           "...¿qué?" ── (<face: skeptical>)   │
│      │                                                          │                                │
│     ╱│╲                                                        ╱│╲                               │
│     ╱ ╲                                                        ╱ ╲                               │
│                                                                                                  │
└──────────────────────────────────────────────────────────────────────────────────────────────────┘

┌── Panel 3: Reveal ──────────────────────────────────────────────────────────────────────────────┐
│                                                                                                  │
│   <Char A name>                                       <Char B name>                              │
│   (<face: dawning>) ── "<the correct rule stated>"           "<correction>" ── (<face: delighted>)│
│      │                                                          │                                │
│     ╱│╲                                                        ╱│╲                               │
│     ╱ ╲                                                        ╱ ╲                               │
│                                                                                                  │
└──────────────────────────────────────────────────────────────────────────────────────────────────┘

┌── Panel 4: Application ─────────────────────────────────────────────────────────────────────────┐
│                                                                                                  │
│   <Char A name>                                                                                  │
│   (<face: happy>) ── "<the corrected line>"                                                      │
│      │                                                                                           │
│     ╱│╲                                                                                          │
│     ╱ ╲                                                                                          │
│                                                                                                  │
└──────────────────────────────────────────────────────────────────────────────────────────────────┘
```

## Short rendered example (A9.2 Contrast arc, 2 panels)

A canonical "ser vs estar" contrast — wrong panel, then right panel.

```
┌── ❌ Panel 1: Wrong way ────────────────────────────────────────────────────────────────────────┐
│                                                                                                  │
│   Priyesh                                                                                        │
│   (•_•) ── "Yo soy 30 años."                                                                     │
│     │                                                                                            │
│    ╱│╲                                                                                           │
│    ╱ ╲                                                                                           │
│                                                                                                  │
│   ┌── narración ──────────────────────────────────────────────────────────────────────────────┐ │
│   │  "Yo soy 30 años" literally means "I AM 30 years" — using ser. Wrong verb.                 │ │
│   └────────────────────────────────────────────────────────────────────────────────────────────┘ │
│                                                                                                  │
└──────────────────────────────────────────────────────────────────────────────────────────────────┘

┌── ✓ Panel 2: Right way ─────────────────────────────────────────────────────────────────────────┐
│                                                                                                  │
│   Priyesh                                                                                        │
│   (•◡•) ── "Tengo 30 años."                                                                      │
│     │                                                                                            │
│    ╱│╲                                                                                           │
│    ╱ ╲                                                                                           │
│                                                                                                  │
│   ┌── narración ──────────────────────────────────────────────────────────────────────────────┐ │
│   │  "Tengo 30 años" = "I HAVE 30 years" — tener for age. Always.                              │ │
│   └────────────────────────────────────────────────────────────────────────────────────────────┘ │
│                                                                                                  │
└──────────────────────────────────────────────────────────────────────────────────────────────────┘
```

## Failure modes

- If user explicitly requests ASCII fallback → fall back to `slideshow` (comic depends on Unicode emoticons + rounded bubble corners that have no clean ASCII equivalents)
- If the topic has no characters and no concept to anthropomorphize → fall back to `slideshow`
- If a panel needs more than 3 characters → split into more panels or use a narration box for context
- If dialogue won't fit at 100 cols → switch the line to a boxed bubble (gains vertical room) or move context to a narration box
- If the same character has the same face in every panel → fail strict QA item 5 → simplify or reroute to slideshow per `qa-checklist.md`
- If the user wants more than 8 panels without explicit request → compress; offer to split into a sequel comic
- If the joke isn't landing in an A9.3 (subjective — skill can't detect) → ship anyway; let user iterate
````

- [ ] **Step 2: Verify width**

Run:
```bash
python3 -c "
import re
c = open('formats/comic.md').read()
blocks = re.findall(r'\`\`\`[a-z]*\n(.*?)\`\`\`', c, re.DOTALL)
for i, b in enumerate(blocks, 1):
    w = max(len(l) for l in b.split('\n')) if b.strip() else 0
    print(f'block {i}: width {w}/100')
"
```
Expected: every block ≤ 100. If any block exceeds, shorten content and re-verify before committing.

- [ ] **Step 3: Verify section structure**

Run:
```bash
grep -c "^## " formats/comic.md
```
Expected: `10` — Purpose, Use when, Do NOT use when, Width budget, Arc, Layout rules, Face library, Canonical skeleton — Unicode, Short rendered example, Failure modes.

- [ ] **Step 4: Commit**

```bash
cd ~/.claude/skills/ascii-canvas && \
  git add formats/comic.md && \
  git commit -m "feat(comic): add comic format spec file"
```

---

# Phase 3 — The example file

## Task 5: Write examples/comic-example.md

**Files:**
- Create: `examples/comic-example.md`

- [ ] **Step 1: Author the file with the full content below**

Richer reference artifact — full 4-panel A9.1 teaching arc on "ser vs estar" with two named characters (Sofía female `(...)`, Carlos male `[...]`).

````markdown
# comic — full example

**Topic:** Ser vs Estar — the classic "Yo soy 30 años" mistake (A9.1 teaching arc, 4 panels)
**Width budget:** 100 cols
**Mode:** Unicode (default — comic doesn't have an ASCII fallback)

---

```
┌── Panel 1: At the language exchange ────────────────────────────────────────────────────────────┐
│                                                                                                  │
│   Sofía                                              Carlos                                      │
│   (•‿•) ── "Hola! ¿Cuántos años tienes?"                            "Hola!" ── [•‿•]             │
│     │                                                                  │                         │
│    ╱│╲                                                                ╱│╲                        │
│    ╱ ╲                                                                ╱ ╲                        │
│                                                                                                  │
└──────────────────────────────────────────────────────────────────────────────────────────────────┘

┌── Panel 2: The mistake ─────────────────────────────────────────────────────────────────────────┐
│                                                                                                  │
│   Sofía                                              Carlos                                      │
│   (¬_¬)                                                       "Yo soy 30 años." ── [•_•]         │
│     │                                                                  │                         │
│    ╱│╲                                                                ╱│╲                        │
│    ╱ ╲                                                                ╱ ╲                        │
│                                                                                                  │
└──────────────────────────────────────────────────────────────────────────────────────────────────┘

┌── Panel 3: The correction ──────────────────────────────────────────────────────────────────────┐
│                                                                                                  │
│   Sofía                                              Carlos                                      │
│   (•‿•) ── ╭───────────────────────────────────────╮              (O_o) ── "Oh."                 │
│              │ Casi! Para la edad usamos TENER,    │                 │                           │
│              │ no SER. Es: 'Tengo 30 años' —       │                ╱│╲                          │
│              │ literalmente, 'I have 30 years.'    │                ╱ ╲                          │
│              ╰───────────────────────────────────────╯                                           │
│     │                                                                                            │
│    ╱│╲                                                                                           │
│    ╱ ╲                                                                                           │
│                                                                                                  │
└──────────────────────────────────────────────────────────────────────────────────────────────────┘

┌── Panel 4: Application ─────────────────────────────────────────────────────────────────────────┐
│                                                                                                  │
│   Sofía                                              Carlos                                      │
│   (•◡•) ── "¡Eso es!"                                       "Tengo 30 años." ── [^_^]            │
│     │                                                                  │                         │
│    ╱│╲                                                                ╱│╲                        │
│    ╱ ╲                                                                ╱ ╲                        │
│                                                                                                  │
│   ┌── narración ──────────────────────────────────────────────────────────────────────────────┐ │
│   │  Rule: edad (age) uses TENER. SER is for identity ("Soy Carlos"), not duration.            │ │
│   └────────────────────────────────────────────────────────────────────────────────────────────┘ │
│                                                                                                  │
└──────────────────────────────────────────────────────────────────────────────────────────────────┘
```

---

## Why this works

- **A9.1 teaching arc** in exactly 4 panels: Sofía's question sets up the situation, Carlos makes the canonical mistake, Sofía corrects with the rule stated explicitly (boxed bubble for the longer explanation), Carlos applies it correctly. Each panel earns its existence per U1.
- **Face progression** carries the emotion arc: Sofía neutral-happy → skeptical → patient → pleased; Carlos cheerful → confident-wrong → surprised → delighted. Mandatory per comic-specific strict QA item 5.
- **Bracket consistency** holds: Sofía always `(...)`, Carlos always `[...]`. Identity readable at a glance even without name labels (which are present in all panels for clarity).
- **Hybrid bubble grammar** in action: inline `── "..."` for short lines, boxed `╭─...─╮` for the longer correction in Panel 3, and a narration box in Panel 4 for the takeaway rule.
- **A9.1 over A9.2** chosen because the topic has a story shape (encounter → mistake → reveal → apply). A9.2 contrast would compress this into 2 panels but loses the dramatic moment of the mistake landing.

## ASCII variant

Comic does not ship an ASCII fallback. The format relies on Unicode emoticons (`(•‿•)` etc.) and rounded bubble corners (`╭╮╰╯`) that have no clean ASCII equivalents preserving the comic feel. If a user requests plain ASCII output, the skill falls back to `slideshow` per the failure-mode in `comic.md` and the format-fallback map in `qa-checklist.md`.
````

- [ ] **Step 2: Verify width**

Run:
```bash
python3 -c "
import re
c = open('examples/comic-example.md').read()
blocks = re.findall(r'\`\`\`[a-z]*\n(.*?)\`\`\`', c, re.DOTALL)
for i, b in enumerate(blocks, 1):
    w = max(len(l) for l in b.split('\n')) if b.strip() else 0
    print(f'block {i}: width {w}/100')
"
```
Expected: every block ≤ 100. Fix and re-verify if any exceed.

- [ ] **Step 3: Commit**

```bash
cd ~/.claude/skills/ascii-canvas && \
  git add examples/comic-example.md && \
  git commit -m "feat(comic): add comic example artifact"
```

---

# Phase 4 — SKILL.md updates

## Task 6: Update SKILL.md — description, routing matrix, tie-breakers

**Files:**
- Modify: `SKILL.md`

- [ ] **Step 1: Read current SKILL.md**

Open `SKILL.md` and locate:
1. The YAML frontmatter `description:` field
2. The "Explicit format requests:" line in the When to fire section
3. The routing matrix in step 2 of the Routing flow
4. The Composition rules section that lists `composition-rules/*.md` files

- [ ] **Step 2: Update the YAML description trigger examples**

Find the `description:` line in the frontmatter. After `... timeline, etc.)`, the trigger description should mention comic explicitly. Update by adding "comic strip" to the explicit-format list. Change the trigger-clause from:

```
... (flowchart, slideshow, cheat sheet, infographic, timeline, etc.) OR asks for ...
```

to:

```
... (flowchart, slideshow, cheat sheet, infographic, timeline, comic strip, etc.) OR asks for ...
```

- [ ] **Step 3: Update the "When to fire — Fire on:" explicit examples**

In the body of SKILL.md, find the bullet:
```
- Explicit format requests: "make a flowchart", "draw the architecture", "ASCII slideshow", "infographic on X", "comparison table", "timeline of", "cheat sheet for"
```

Replace it with:
```
- Explicit format requests: "make a flowchart", "draw the architecture", "ASCII slideshow", "infographic on X", "comparison table", "timeline of", "cheat sheet for", "make a comic", "comic strip", "comic-style", "as a skit", "as a scenario", "with characters", "dialogue between X and Y", "anthropomorphize X"
```

- [ ] **Step 4: Update the routing matrix**

Find the routing-matrix code block (it begins with `branching + decisions         → decision-tree`). Add these two rows at the bottom of the matrix, before the closing tie-breakers section:

```
   characters + dialogue + lesson      → comic
   anthropomorphized concept           → comic
```

- [ ] **Step 5: Update the tie-breakers**

Find the existing tie-breakers section (begins `Tie-breakers:`). Add these two lines immediately after the existing three tie-breaker lines, BEFORE the line `   - Do NOT combine formats in v1 unless explicitly requested`:

```
   - Comic vs slideshow ambiguous     → slideshow (simpler)
   - Comic vs sequence-diagram        → comic for educational, sequence-diagram for technical
```

- [ ] **Step 6: Verify**

Run:
```bash
grep -c "comic" SKILL.md
```
Expected: at least 6 (description, explicit triggers, 2 routing matrix rows, 2 tie-breakers).

Run:
```bash
grep -c "characters + dialogue + lesson" SKILL.md
```
Expected: `1`

- [ ] **Step 7: Commit**

```bash
cd ~/.claude/skills/ascii-canvas && \
  git add SKILL.md && \
  git commit -m "feat(comic): wire comic into SKILL.md routing + triggers"
```

---

# Phase 5 — Acceptance suite

## Task 7: Run 3 comic-specific prompts + spot-check 3 existing prompts

**Files:**
- Create: `docs/comic-acceptance-results.md`

This is the verification step. The format is built; now confirm end-to-end behavior.

- [ ] **Step 1: Run prompt C1 — A9.1 teaching arc**

Prompt to run (in a fresh Claude session with the updated skill installed):

> Make me a comic teaching the ser vs estar mistake.

**Structural expectations:**
- (a) routes to comic format (not slideshow)
- (b) A9.1 teaching arc: 3–5 panels, default 4
- (c) two named characters with consistent bracket types throughout (e.g., Sofía `(...)`, Carlos `[...]`)
- (d) face moods change across panels for each character (strict QA item 5)
- (e) at least one panel has dialogue that lands the rule (the "reveal" panel)
- (f) max line width ≤ 100
- (g) file auto-saved to `~/Ascii-diagrams/YYYY-MM/YYYY-MM-DD-<slug>.md`

- [ ] **Step 2: Run prompt C2 — A9.2 contrast arc**

Prompt:

> Comic-style ❌/✓ on tú vs usted.

**Structural expectations:**
- (a) routes to comic format
- (b) A9.2 contrast arc: exactly 2 panels (one ❌, one ✓)
- (c) panel titles include `❌` and `✓` markers
- (d) reaction faces communicate wrong-vs-right (skeptical/mortified for ❌, dawning/delighted for ✓)
- (e) max line width ≤ 100
- (f) file auto-saved (multi-panel)

- [ ] **Step 3: Run prompt C3 — A9.4 tech-explainer arc**

Prompt:

> Anthropomorphize Stripe webhook signature verification as a comic.

**Structural expectations:**
- (a) routes to comic format
- (b) A9.4 tech-explainer arc: 4 panels
- (c) anthropomorphized character uses angle-bracket glyph `<Webhook>` (and/or `<Stripe>`, `<Signature>`)
- (d) at least one panel has a narration box (top OR bottom) framing the technical concept
- (e) panel 1 establishes the actors, panel 4 lands the resolution/takeaway
- (f) max line width ≤ 100
- (g) file auto-saved

- [ ] **Step 4: Spot-check 3 existing prompts (regression test)**

Run these 3 existing v1.0.0 prompts to confirm comic addition didn't break anything:

> R1: "Make me a flowchart of how user signup works in a typical web app."

Expected: routes to flowchart, single-artifact, ≤100 cols, no file saved. Same as v1.0.0 acceptance.

> R2: "What year did Vercel acquire next.js?"

Expected: skill does NOT activate. Plain prose response. No box-drawing, no `## Section` headings.

> R3: "Give me a playbook for cold outbound — keep it useful, not generic."

Expected: routes to playbook (NOT comic, even though "useful" hints at engaging content). Auto-saves. ≤80 cols.

- [ ] **Step 5: Document results**

Write `docs/comic-acceptance-results.md`:

````markdown
# Comic format acceptance suite — 2026-05-18

## Prompt C1 (A9.1 teaching arc)

**Prompt:** Make me a comic teaching the ser vs estar mistake.
**Expected:** comic format, 4-panel teaching arc, 2 named characters, faces change, ≤100 cols, file saved
**Observed:** <fill in>
**Structural checks:** (a) PASS/FAIL ... (g) PASS/FAIL
**Verdict:** PASS / FAIL

## Prompt C2 (A9.2 contrast arc)

[Same structure as C1]

## Prompt C3 (A9.4 tech-explainer arc)

[Same structure as C1]

## Regression R1 (flowchart, no save)

[Same structure]

## Regression R2 (non-activation on factual question)

[Same structure]

## Regression R3 (playbook, not comic)

[Same structure]

## Summary

- Comic prompts: N/3 pass
- Regression prompts: N/3 pass
- Issues to fix: <list or "none">
````

- [ ] **Step 6: Fix any failures**

For each FAIL:
- Identify which file caused the issue (SKILL.md routing, formats/comic.md, narrative-arcs.md, qa-checklist.md)
- Edit that file with `fix: <description>` commit
- Re-run the failing prompt
- Update results doc

Iterate until 6/6 pass.

- [ ] **Step 7: Commit acceptance results**

```bash
cd ~/.claude/skills/ascii-canvas && \
  git add docs/comic-acceptance-results.md && \
  git commit -m "docs: record comic format acceptance suite results"
```

- [ ] **Step 8: Tag v1.1.0**

Only after 6/6 prompts pass:

```bash
cd ~/.claude/skills/ascii-canvas && \
  git tag -a v1.1.0 -m "ascii-canvas v1.1.0 — add comic format (17 formats, A9 arc family, comic-specific strict QA)"
```

---

# Done criteria

The implementation is v1.1.0-complete when:

1. All 7 tasks completed with clean commits
2. `git log --oneline` shows ~8 new commits since v1.0.0 (one per task + the spec commit already on main)
3. All 6 acceptance prompts pass (3 comic-specific + 3 regression)
4. Strict QA correctly catches a static-face comic (manual test: ask for a comic where every panel uses the same face → expect fail-twice → reroute to slideshow with the simplified-from note)
5. Repository tagged `v1.1.0`
6. The `ascii-canvas` skill description in SKILL.md frontmatter mentions comic as a trigger keyword (so it auto-fires on future sessions)

---

# File summary

**New (2 files):**
- `formats/comic.md`
- `examples/comic-example.md`

**Modified (4 files):**
- `composition-rules/width-budgets.md`
- `composition-rules/narrative-arcs.md`
- `composition-rules/qa-checklist.md`
- `SKILL.md`

**Added in docs (1 file):**
- `docs/comic-acceptance-results.md`

**Already committed (1 file):**
- `docs/2026-05-18-comic-format-design.md` (the spec, committed before this plan was executed)

**Total: 7 files touched, ~8 commits, 1 new tag.**
