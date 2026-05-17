# slideshow

## Purpose

Multi-panel narrative explainer that walks the reader through a concept slide-by-slide.

## Use when

- Teaching a concept to an audience that needs to be walked through it step by step
- A user asks "make me a slideshow on X" or "turn this into slides"
- Turning a topic into shareable, digestible panels for a thread or post
- Building an explainer with a hook, development, and takeaway arc

## Do NOT use when

- Compressing everything into one dense image-like artifact — use `infographic`
- Documenting a repeatable SOP or workflow — use `playbook`
- Teaching a skill with progressive difficulty levels — use `learning-ladder`

## Width budget

80 cols

## Arc

A1 — Slideshow arc (5–7 panels): hook → context → core idea → 2 examples → takeaway → optional recap

## Layout rules

- One panel per `## Slide N — <title>` heading
- Each panel wrapped in a 78-col-wide framed box (1 col padding each side within 80-col budget)
- Top border: `┌` + 76× `─` + `┐`  (total: 78 cols)
- Content lines: `│ ` + up to 74 content chars + ` │`  (total: 78 cols)
- Bottom border: `└` + 76× `─` + `┘`  (total: 78 cols)
- Panel titles left-aligned inside the box, consistent style
- Body uses single bullet style throughout (no mixing bold headers with plain bullets)
- Slides separated by a blank line, `---`, and another blank line in the saved `.md`

## Canonical skeleton — Unicode

## Slide 1 — Hook

```
┌────────────────────────────────────────────────────────────────────────────┐
│ Slide 1 — Hook                                                             │
│                                                                            │
│ • Opening statement that grabs attention                                   │
│ • One supporting line that earns the next slide                            │
└────────────────────────────────────────────────────────────────────────────┘
```

---

## Slide 2 — Context

```
┌────────────────────────────────────────────────────────────────────────────┐
│ Slide 2 — Context                                                          │
│                                                                            │
│ • Why this topic matters now                                               │
│ • One concrete framing detail                                              │
│ • Bridges to the core idea in Slide 3                                      │
└────────────────────────────────────────────────────────────────────────────┘
```

## Canonical skeleton — ASCII fallback

## Slide 1 — Hook

```
+----------------------------------------------------------------------------+
| Slide 1 -- Hook                                                            |
|                                                                            |
| * Opening statement that grabs attention                                   |
| * One supporting line that earns the next slide                            |
+----------------------------------------------------------------------------+
```

---

## Slide 2 — Context

```
+----------------------------------------------------------------------------+
| Slide 2 -- Context                                                         |
|                                                                            |
| * Why this topic matters now                                               |
| * One concrete framing detail                                              |
| * Bridges to the core idea in Slide 3                                      |
+----------------------------------------------------------------------------+
```

## Short rendered example

A 3-panel excerpt on "Why ASCII diagrams beat screenshots for documentation":

```
┌────────────────────────────────────────────────────────────────────────────┐
│ Slide 1 -- The screenshot trap                                             │
│                                                                            │
│ • Screenshots look good on day one. By day 30 they are wrong.              │
│ • Every UI change breaks your docs silently.                               │
│ • You cannot diff an image in a pull request.                              │
└────────────────────────────────────────────────────────────────────────────┘
```

---

```
┌────────────────────────────────────────────────────────────────────────────┐
│ Slide 2 -- What ASCII diagrams do differently                              │
│                                                                            │
│ • Plain text lives in the same repo as the code it documents.              │
│ • Reviewers can read, edit, and comment on it line by line.                │
│ • No tooling required -- renders in any terminal or markdown viewer.       │
└────────────────────────────────────────────────────────────────────────────┘
```

---

```
┌────────────────────────────────────────────────────────────────────────────┐
│ Slide 3 -- The rule                                                        │
│                                                                            │
│ • If the diagram needs to stay accurate: use ASCII.                        │
│ • If it needs to look beautiful once: use a screenshot.                    │
│ • Accuracy compounds. Beauty decays.                                       │
└────────────────────────────────────────────────────────────────────────────┘
```

## Failure modes

- If content doesn't fill 5+ panels → reduce panel count; do not add filler slides (per U4 in narrative-arcs.md)
- If a single panel's body overflows the 76-char content width → break body across 2 slides
- If the topic has no narrative arc (e.g. a reference list) → fall back to `infographic`
- If bullets per slide exceed ~6 → split the slide; dense slides defeat the format's purpose
