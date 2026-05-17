# Narrative arcs (multi-panel formats)

Every multi-panel format has a canonical arc — a fixed sequence of panel purposes. The format file references its arc by name.

## The 8 arcs

### A1 — Slideshow arc (5–7 panels)

1. Hook / framing
2. Context / why it matters
3. Core idea
4. Example #1
5. Example #2
6. Key takeaway
7. *Optional:* recap or next step

**Use for:** teaching concepts, content posts, explainers.

### A2 — Playbook arc (5–8 panels)

1. Objective
2. When to use / context
3. Prerequisites
4. Step 1 of execution
5. Step 2 of execution
6. Step N of execution
7. Success criteria
8. Failure modes / pitfalls

**Use for:** workflows, SOPs, AI agent systems, marketing execution.

### A3 — Learning-ladder arc (4–6 levels)

1. Foundations
2. Core mechanics
3. Practical application
4. Intermediate depth
5. Advanced nuance
6. Expert / edge cases

**Use for:** skill progression, education.

### A4 — Infographic arc (4–6 blocks)

1. Headline / key claim
2. Supporting insight #1
3. Supporting insight #2
4. Supporting insight #3
5. Synthesis / takeaway
6. *Optional:* CTA / action

**Use for:** high-signal summaries, social content.

### A5 — Concept-stack arc (4–6 layers)

1. Base layer (foundation)
2. Supporting layer
3. Supporting layer
4. Supporting layer
5. Top-level outcome

**Use for:** systems thinking, dependencies, architecture of ideas.

### A6 — Content-map arc (3–5 clusters)

1. Core idea
2. Angle cluster #1 (with hooks/posts/threads underneath)
3. Angle cluster #2
4. Angle cluster #3
5. *Optional:* distribution notes

**Use for:** content expansion, social idea trees.

### A7 — Dashboard arc (4–8 panels)

1. Title / context
2. Key metric block
3. Key metric block
4. Key metric block
5. Summary / signal

**Use for:** status views, performance summaries.

### A8 — Step-by-step-guide arc (4–7 steps)

1. Goal
2. Step 1
3. Step 2
4. Step 3
5. Outcome / verification

**Use for:** simple processes (lighter than playbook).

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

## Universal panel rules (apply to every arc)

### U1 — Every panel must earn its existence

If two panels say similar things → merge. If a panel has weak content → drop.

### U2 — Transition rule

Panel N must logically create the need for Panel N+1. If not, structure is wrong — reorder or rewrite.

### U3 — Default panel count

4–7 panels. Never exceed 9 without explicit user request. **Compress before expanding.**

### U4 — Content-driven reduction

If content doesn't justify the full arc → reduce panel count. **Do NOT introduce filler** to meet default ranges.

### U5 — User override

If user specifies structure ("3 slides", "5 steps") → follow user verbatim. Override default arc length.

### U6 — Format ≠ layout

Each format is a **way of organizing thinking**, not just visual furniture:
- Slideshow = narrative
- Playbook = execution
- Learning-ladder = progression
- Infographic = compression
- Concept-stack = dependency
- Content-map = expansion
- Dashboard = surveillance
- Step-by-step-guide = sequence

If the chosen format doesn't match the topic's *thinking shape*, switch formats.
