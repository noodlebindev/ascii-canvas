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
