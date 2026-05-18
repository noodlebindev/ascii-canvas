---
name: ascii-canvas
description: Compose ASCII/Unicode diagrams, slideshows, infographics, playbooks, comic strips, flashcards, and other text-based visual artifacts from a topic, idea, or set of facts. Use when the user explicitly requests a diagram/visual/format (flowchart, slideshow, cheat sheet, infographic, timeline, comic strip, flashcards, etc.) OR asks for a structured breakdown / step-by-step explanation of a non-trivial topic. Do NOT trigger for simple factual questions, short answers (less than ~3 steps or one paragraph), or conversational/opinion queries.
---

# ascii-canvas

Compose high-quality ASCII/Unicode text-based visual artifacts. "Canva for ASCII."

## When to fire

**Fire on:**
- Explicit format requests: "make a flowchart", "draw the architecture", "ASCII slideshow", "infographic on X", "comparison table", "timeline of", "cheat sheet for", "make a comic", "comic strip", "comic-style", "as a skit", "as a scenario", "with characters", "dialogue between X and Y", "anthropomorphize X", "make flashcards", "flashcard deck", "vocab cards", "study cards", "Anki-style cards", "drill me on X", "quiz me on X", "test me on X", "help me memorize X"
- Visual framing: "visualize X", "show me how X works", "diagram this", "illustrate"
- Structured breakdown of non-trivial topics: "break down X", "walk me through X step by step", "explain X as a playbook", "learning ladder for X", "content map for X"

**Do NOT fire on:**
- Simple factual questions ("what year did X happen?")
- Short answers (less than ~3 steps or one paragraph)
- Conversational replies, opinions, hot takes
- When trigger is weak AND structure won't improve clarity over prose

## Routing flow

```
1. DETECT TRIGGER
   ├── Explicit format keyword?        → load that format file
   ├── Visual framing?                 → infer format from topic shape (matrix below)
   ├── Structured breakdown of
   │   non-trivial topic?              → infer multi-panel format
   └── None / weak / won't help        → DO NOT activate; respond as plain prose

2. CHOOSE FORMAT
   If user named one → use it.
   Otherwise apply the routing matrix:

   branching + decisions         → decision-tree
   branching + mixed steps       → flowchart
   linear process                → step-by-step-guide
   repeatable workflow / SOP     → playbook
   skill progression             → learning-ladder
   one idea → many outputs       → content-map
   layers / dependencies         → concept-stack
   side-by-side options          → comparison-table
   actors + messages             → sequence-diagram
   system components             → architecture-diagram
   events over time              → timeline
   central idea + radial         → mind-map
   dense reference               → cheat-sheet
   status / metrics              → dashboard
   narrative explainer           → slideshow
   high-signal summary           → infographic
   characters + dialogue + lesson → comic
   anthropomorphized concept     → comic
   recall / memorization drill   → flashcards
   quiz / test self              → flashcards

   Tie-breakers:
   - Multiple formats apply       → choose simplest that preserves clarity
   - Two formats equally fit      → choose the simpler one
   - Comic vs slideshow ambiguous → slideshow (simpler)
   - Comic vs sequence-diagram    → comic for educational, sequence-diagram for technical
   - Flashcards vs cheat-sheet    → flashcards for active recall, cheat-sheet for passive reference
   - Flashcards vs comparison-table → comparison-table for side-by-side, flashcards for sequential Q/A
   - Do NOT combine formats in v1 unless explicitly requested

3. LOAD FORMAT FILE (MANDATORY)
   → Read /Users/priyeshpatel/Skills/ascii-canvas/formats/<format>.md
   No ad-hoc layouts. Templates only.

4. DETERMINE CHARACTER SET
   Unicode by default. ASCII fallback if user requested OR destination demands.
   See composition-rules/box-drawing.md.

5. APPLY CANONICAL ARC (multi-panel formats only)
   See composition-rules/narrative-arcs.md.
   Reduce panel count if content doesn't justify the full arc.

6. GENERATE OUTPUT

7. DETERMINE SAVE BEHAVIOR
   - Single-artifact + not multi-section + not "reusable asset" → chat only
   - Multi-panel / multi-section / clearly reusable → auto-save
   - User signaled iteration ("try again", "draft") → chat only
   - User said "save this" → force save
   - User said "don't save" / "chat only" → force chat

8. RUN QA
   - Strict mode for saved/multi-panel/reusable
   - Light mode otherwise
   - Strict QA must pass BEFORE chat render AND BEFORE file write
   - If fails twice → invoke simplify rule
   - If simplify still fails → invoke format fallback (see qa-checklist.md)

9. RENDER + (optional) SAVE
   - Chat preview: ≤80 lines → render full. >80 lines → render first 1-2 sections + "saved to <path>"
   - File write: only AFTER strict QA passes. Path: ~/Ascii-diagrams/YYYY-MM/YYYY-MM-DD-<slug>.md
   - Post-save line: exactly two lines, no fluff:
       Saved to:
       ~/Ascii-diagrams/YYYY-MM/YYYY-MM-DD-<slug>.md
```

## Output behavior

### Save path & naming

- Path: `~/Ascii-diagrams/YYYY-MM/YYYY-MM-DD-<topic-slug>.md`
- Slug: lowercase, hyphen-separated, 6–8 words max, derived from user intent
- Fallback slug if user intent is unclear: `<format>-<short-topic>` (e.g., `playbook-cold-outbound`)

### File template

```markdown
# Title

Short description (1–2 lines)

---

## Section 1

<ASCII inside a code block>

---

## Section 2

<ASCII>
```

### Chat preview rules

- ≤80 lines → render the full artifact inline
- >80 lines → render the first 1–2 sections + emit:
  ```
  Full artifact saved to:
  ~/Ascii-diagrams/2026-05/2026-05-17-<slug>.md
  ```
- Offer "expand to show full" only if the user might want it inline

### Anti-pattern

Do NOT default to saving everything "just in case." Throwaway sketches do not deserve files. Noise > occasional regret.

## Composition rules (read on demand)

- `composition-rules/box-drawing.md` — Unicode set, ASCII fallback, consistency rules
- `composition-rules/width-budgets.md` — per-format max width + overflow handling
- `composition-rules/narrative-arcs.md` — 8 arcs + universal panel rules
- `composition-rules/qa-checklist.md` — light/strict QA + simplify + fallback + no-partial-save

## Examples (read on demand)

`examples/<format>-example.md` — one richer reference per format. Read when the format file's inline example isn't enough.

## v1 boundaries (explicitly out of scope)

- `mode: quick | publish` flag → v2
- External tools (graph-easy, ditaa, figlet) → manual workflow only, not integrated
- Color / ANSI escapes → not used
- Image export → not in scope
- Format combination (e.g. slideshow with embedded flowchart) → only when explicitly requested

## Hard rules (do not violate)

1. **Always load the relevant format file before rendering output.** No ad-hoc layouts.
2. **Strict QA must pass before any file write.** No partial saves. No QA-failed saves.
3. **Never exceed format max width.** Shrink content; never widen past budget.
4. **Default to saving NOTHING.** Save only what matches the save criteria.
5. **Format choice: simplest that preserves clarity.** No combining formats in v1 unless asked.
