# infographic — full example

**Topic:** Why ASCII beats screenshots for code docs — 3 stats + synthesis + CTA
**Width budget:** 100 cols
**Mode:** Unicode (default)

---

```
╔══════════════════════════════════════════════════════════════════════════════════════════════════╗
║                         ASCII > SCREENSHOTS FOR CODE DOCUMENTATION                               ║
╚══════════════════════════════════════════════════════════════════════════════════════════════════╝
┌──────────────────────────────┬──────────────────────────────┬──────────────────────────────────┐
│                              │                              │                                  │
│     ◆  100% PORTABLE         │     ▲  10× SMALLER           │     ●  ALWAYS EDITABLE           │
│                              │                              │                                  │
│  Renders in any editor,      │  Kilobytes vs megabytes.     │  Diff-able in pull requests.     │
│  terminal, Slack, GitHub,    │  A 30-box architecture       │  Change a label in 5 seconds.    │
│  or email — no tooling       │  diagram is < 4 KB of        │  No image editor, no             │
│  required                    │  plain text                  │  screenshot re-take needed       │
│                              │                              │                                  │
└──────────────────────────────┴──────────────────────────────┴──────────────────────────────────┘
┌──────────────────────────────────────────────────────────────────────────────────────────────────┐
│  Screenshots are dead weight. They age like milk, live outside the repo, and break silently     │
│  when the UI changes. ASCII diagrams age like code — they travel with the codebase, degrade    │
│  gracefully, and stay accurate as long as the engineer cares enough to update one line.         │
└──────────────────────────────────────────────────────────────────────────────────────────────────┘
                                    → Try it: /ascii-canvas
```

---

## Why this works

- Three supporting blocks (portability, size, editability) address the three objections engineers raise to adopting ASCII diagrams: "will it render?", "is it worth the file size?", and "how hard is maintenance?" — each block neutralises one objection directly.
- The synthesis box carries two sentences instead of the skeleton's one because the topic needs a villain (screenshots) and a hero (ASCII) to make the argument land; a one-liner would feel like a slogan without context.
- The CTA is minimal (`/ascii-canvas`) rather than a URL, reinforcing that this is a tool-native skill, not a marketing page.
