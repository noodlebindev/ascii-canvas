# ascii-canvas

> Canva for ASCII. Compose diagrams, slideshows, infographics, playbooks,
> comic strips, flashcards, and other text-based visual artifacts from any
> topic, idea, or set of facts.

A Claude Code skill that turns prose requests like "make me a flowchart of
user signup" or "drill me on Spanish verbs" into clean, rendered ASCII/Unicode
artifacts with strict width budgets, canonical narrative arcs, and auto-save
to a date-organized library.

## Install

Clone into Claude Code's skills directory:

```bash
git clone <repo-url> ~/.claude/skills/ascii-canvas
```

That's it. Claude Code auto-discovers the skill at session start.

## Usage

The skill auto-fires when your prompt matches its triggers, or you can invoke
explicitly with `/ascii-canvas`:

```
"Make me a flowchart of how Stripe webhooks handle idempotency."
"Break down Spanish verb conjugation visually."
"Comic teaching the ser vs estar mistake."
"Flashcards for the 12 most common Spanish verbs."
"Drill me on Next.js hooks."
"Dashboard of weekly metrics."
"Architecture diagram of a Vercel + Neon Postgres app, in plain ASCII for email."
```

Outputs render inline in chat. Multi-panel artifacts auto-save to
`~/Ascii-diagrams/YYYY-MM/YYYY-MM-DD-<slug>.md` for reuse.

## The 18 formats

| Format | Use case |
|---|---|
| `flowchart` | Mixed processes with steps + branches |
| `step-by-step-guide` | Simple linear walkthroughs |
| `timeline` | Events on an axis |
| `comparison-table` | 2–5 options side by side |
| `architecture-diagram` | System components + connections |
| `sequence-diagram` | Actors + time-ordered messages |
| `mind-map` | Central idea + radial branches |
| `cheat-sheet` | Dense reference card |
| `slideshow` | Narrative explainer, multi-panel |
| `infographic` | Headline + supporting blocks + synthesis |
| `dashboard` | Metrics / status board |
| `decision-tree` | Yes/no branching to outcomes |
| `learning-ladder` | Beginner → expert progression |
| `playbook` | SOPs, repeatable workflows |
| `content-map` | One idea → many posts/threads |
| `concept-stack` | Layered dependencies |
| `comic` | Characters + dialogue lessons |
| `flashcards` | Vocab + concept cards w/ drill file + chat quiz |

See the routing matrix in `SKILL.md` for which format the skill picks based
on phrasing.

## What's inside

```
ascii-canvas/
├── SKILL.md                       # entry point: triggers, routing, output rules
├── formats/                       # 18 format spec files
├── composition-rules/             # box-drawing, width budgets, narrative arcs, QA
├── examples/                      # 18 richer reference artefacts
└── docs/                          # design specs, implementation plans, acceptance results
```

## Design principles

- **Pure Claude generation.** No external CLI tools (no graph-easy, ditaa,
  figlet). The skill is a markdown bundle, zero install friction.
- **Strict width discipline.** Every format declares a width budget (80, 100,
  or 120 cols). Strict QA verifies before render and before file write.
- **Format-fallback graceful degradation.** If a chosen format can't be
  rendered cleanly, the skill falls back to a simpler adjacent format (e.g.
  `comic → slideshow` if there are no characters to anthropomorphize).
- **Auto-save for reusable artefacts.** Multi-panel outputs land in
  `~/Ascii-diagrams/`. Single-shot diagrams stay in chat — no filesystem
  noise.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). The format-authoring workflow
(brainstorm → spec → plan → execute) is documented in `docs/`.

For security issues, please follow [SECURITY.md](SECURITY.md) — do not file
public issues for vulnerabilities.

## License

MIT — see [LICENSE](LICENSE).
