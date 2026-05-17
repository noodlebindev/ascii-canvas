# slideshow — full example

**Topic:** Why ASCII diagrams beat screenshots for documentation
**Width budget:** 80 cols
**Mode:** Unicode (default)

---

## Slide 1 — The screenshot trap

```
┌────────────────────────────────────────────────────────────────────────────┐
│ Slide 1 — The screenshot trap                                              │
│                                                                            │
│ • You write docs. You paste a screenshot. It looks great.                 │
│ • Three months later: the UI changed. Your screenshot is a lie.           │
│ • Nobody noticed. Nobody updated it. The docs rot silently.               │
│                                                                            │
│ This is the default state of most technical documentation.                │
└────────────────────────────────────────────────────────────────────────────┘
```

---

## Slide 2 — Why screenshots break

```
┌────────────────────────────────────────────────────────────────────────────┐
│ Slide 2 — Why screenshots break                                            │
│                                                                            │
│ • Images are opaque: you can't diff them in a pull request.               │
│ • Screenshots live outside the repo — or as binaries inside it.           │
│ • Reviewers cannot comment on a specific box or arrow.                    │
│ • AI tools cannot read them reliably.                                     │
│ • Every tool upgrade, theme change, or layout shift breaks the image.     │
└────────────────────────────────────────────────────────────────────────────┘
```

---

## Slide 3 — What ASCII diagrams do differently

```
┌────────────────────────────────────────────────────────────────────────────┐
│ Slide 3 — What ASCII diagrams do differently                               │
│                                                                            │
│ • Plain text. Lives in the same file as the code it describes.            │
│ • Fully diffable: every change shows in git blame.                        │
│ • Reviewers can comment on line 42 of a diagram.                          │
│ • Renders in any terminal, editor, Slack, GitHub, or email.               │
│ • AI can read, edit, and generate them.                                   │
└────────────────────────────────────────────────────────────────────────────┘
```

---

## Slide 4 — Example: before (screenshot)

```
┌────────────────────────────────────────────────────────────────────────────┐
│ Slide 4 — Example: before (screenshot)                                     │
│                                                                            │
│  [screenshot: flowchart.png — 280 KB, last modified 14 months ago]        │
│                                                                            │
│  Problems:                                                                 │
│  • 280 KB of binary in the repo                                           │
│  • Nobody knows if it still matches the code                              │
│  • Broken in dark mode                                                    │
│  • Can't be updated without the original tool installed                   │
└────────────────────────────────────────────────────────────────────────────┘
```

---

## Slide 5 — Example: after (ASCII diagram)

```
┌────────────────────────────────────────────────────────────────────────────┐
│ Slide 5 — Example: after (ASCII diagram)                                   │
│                                                                            │
│  ┌──────────┐     ┌──────────┐     ┌──────────┐                           │
│  │  Submit  │──►  │ Validate │──►  │  Create  │                           │
│  │   form   │     │  input   │     │  account │                           │
│  └──────────┘     └────┬─────┘     └──────────┘                           │
│                        │ invalid                                           │
│                   ┌────▼────────────┐                                     │
│                   │  Return errors  │                                     │
│                   └─────────────────┘                                     │
│                                                                            │
│  3 lines changed in the last PR. All visible in the diff.                 │
└────────────────────────────────────────────────────────────────────────────┘
```

---

## Slide 6 — The rule

```
┌────────────────────────────────────────────────────────────────────────────┐
│ Slide 6 — The rule                                                         │
│                                                                            │
│ Use ASCII when the diagram needs to stay accurate over time.              │
│ Use a screenshot when it needs to look pixel-perfect once.                │
│                                                                            │
│ • ASCII diagrams age like code.                                           │
│ • Screenshots age like milk.                                              │
│                                                                            │
│ Accuracy compounds. Beauty decays.                                        │
└────────────────────────────────────────────────────────────────────────────┘
```

---

## Slide 7 — Next step

```
┌────────────────────────────────────────────────────────────────────────────┐
│ Slide 7 — Next step                                                        │
│                                                                            │
│ Pick one diagram in your docs that is a screenshot.                       │
│                                                                            │
│ Replace it with an ASCII version today.                                   │
│                                                                            │
│ • Takes 10 minutes.                                                       │
│ • Your future self will thank you.                                        │
│ • Your reviewers will be able to comment on it.                           │
│                                                                            │
│ → /ascii-canvas — ask Claude to draw it for you                           │
└────────────────────────────────────────────────────────────────────────────┘
```

---

## Why this works

- Seven panels follow the A1 arc precisely: hook (the trap) → context (why screenshots break) → core idea (what ASCII does differently) → two worked examples (before/after) → takeaway (the rule) → call to action (next step).
- Each panel is a 78-col-wide box (76 dashes inner) so all panels share identical width — strict QA passes on cross-artifact consistency.
- Slide 5's embedded mini-diagram fits within 74 inner chars; the boxes were kept to 10 cols wide to avoid overflow.
