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
git clone https://github.com/noodlebindev/ascii-canvas ~/.claude/skills/ascii-canvas
```

That's it. Claude Code auto-discovers the skill at session start.

## Usage

The skill auto-fires when your prompt matches its triggers, or you can invoke
explicitly with `/ascii-canvas`. Some examples of what it's useful for:

**Software & systems**

```
"Architecture diagram of a typical web app with a cache, queue, and workers."
"Sequence diagram of the OAuth 2.0 authorization code flow."
"Flowchart for retrying a failed webhook with exponential backoff."
"Decision tree for choosing between SQL, NoSQL, and a vector database."
"Cheat sheet for git rebase, including interactive mode."
```

**Learning & teaching**

```
"Flashcards for the 50 most common French verbs."
"Drill me on JavaScript array methods."
"Learning ladder from beginner to advanced in statistics."
"Comic explaining why TCP needs a three-way handshake."
"Mind map of the causes of World War I."
```

**Work & operations**

```
"Playbook for onboarding a new engineer in their first week."
"Dashboard of weekly product metrics."
"Timeline of a 12-week product launch."
"Comparison table: Notion vs Linear vs Jira for a 10-person team."
"Step-by-step guide to running a customer discovery interview."
```

**Thinking & writing**

```
"Infographic summarizing the key findings of a research paper."
"Content map: turn one essay on deep work into a thread, video outline, and email."
"Concept stack of the modern web — DNS, TLS, HTTP, HTML."
"Mind map of arguments for and against the four-day workweek."
```

Outputs render inline in chat. Multi-panel artifacts auto-save to
`~/Ascii-diagrams/YYYY-MM/YYYY-MM-DD-<slug>.md` for reuse.

## Sample output

A few inline examples of what the skill produces. See `examples/` for one richer
artifact per format.

### Comparison table

```
REST vs GraphQL vs gRPC

┌──────────────┬──────────────────────┬──────────────────────┬──────────────────────┐
│ Dimension    │ REST                 │ GraphQL              │ gRPC                 │
├──────────────┼──────────────────────┼──────────────────────┼──────────────────────┤
│ Transport    │ HTTP/1.1             │ HTTP/1.1             │ HTTP/2               │
│ Payload      │ JSON                 │ JSON                 │ Protobuf (binary)    │
│ Schema       │ Optional (OpenAPI)   │ Required             │ Required (.proto)    │
│ Caching      │ Easy (HTTP)          │ Harder               │ Custom               │
│ Best for     │ Public APIs          │ Mobile + over-fetch  │ Internal RPC, perf   │
└──────────────┴──────────────────────┴──────────────────────┴──────────────────────┘
```

### Flashcards (single card, front + back)

```
┌─ Card 1 ─────────────────────────────────────────────────────────────────────┐
│                                                                              │
│             ser                                                              │
│             v.                                                               │
│                                                                              │
╞══════════════════════════════════════════════════════════════════════════════╡
│                                                                              │
│   Meaning:   to be (identity, essence, permanence)                           │
│   Example:   Soy Carlos.  →  I am Carlos.                                    │
│   Hook:      ser = WHO you are                                               │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

A drill file (fronts only, for self-testing) auto-generates alongside the
review file.

### Comic (2 panels of 4)

```
┌── Panel 1: At the language exchange ────────────────────────────────────────────────────────────┐
│                                                                                                 │
│   Sofía                                            Carlos                                       │
│   (•‿•) ── "¡Hola! ¿Cuántos años tienes?"                                "¡Hola!" ── [•‿•]      │
│     │                                                                       │                   │
│    ╱│╲                                                                     ╱│╲                  │
│    ╱ ╲                                                                     ╱ ╲                  │
│                                                                                                 │
└─────────────────────────────────────────────────────────────────────────────────────────────────┘

┌── Panel 2: The mistake ─────────────────────────────────────────────────────────────────────────┐
│                                                                                                 │
│   Sofía                                            Carlos                                       │
│   (¬_¬)                                                       "Yo soy 30 años." ── [•_•]        │
│     │                                                                       │                   │
│    ╱│╲                                                                     ╱│╲                  │
│    ╱ ╲                                                                     ╱ ╲                  │
│                                                                                                 │
└─────────────────────────────────────────────────────────────────────────────────────────────────┘
```

Character grammar uses brackets for identity: `(face)` round = female, `[face]`
square = male. The full 4-panel arc (setup → mistake → correction → application)
is in `examples/comic-example.md`.

### Dashboard

```
╔══════════════════════════════════════════════════════════════════════════════════════════════════╗
║  WEEKLY METRICS                                                              as of 2026-05-18    ║
╚══════════════════════════════════════════════════════════════════════════════════════════════════╝
┌────────────────────────────────┬────────────────────────────────┬────────────────────────────────┐
│ Signups (week)                 │ MRR                            │ Churn                          │
│                  312  ▲        │              $18,420  ▲        │                  1.8%  ▼       │
│  +12% vs last week             │  +6% MoM ($1,040 added)        │  down from 2.4% last month     │
├────────────────────────────────┼────────────────────────────────┼────────────────────────────────┤
│ Active users                   │ Top feature                    │ Top referrer                   │
│               2,847  ▲         │             Quick-add  ▬       │       hackernews.com  ▬        │
│  +89 new this week             │  used by 64% of active users   │  142 visits this week          │
└────────────────────────────────┴────────────────────────────────┴────────────────────────────────┘
  Summary: Growth and retention both up; churn at a 6-month low.
```

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
