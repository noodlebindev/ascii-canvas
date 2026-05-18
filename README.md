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

A few inline examples. These aren't here to show what the skill can draw —
they're here to show what it can help you *think*. Each artifact is a
thinking tool first, an illustration second.

### AI agent organigram

```
                                    ┌──────────────────────┐
                                    │     User request     │
                                    └───────────┬──────────┘
                                                ▼
                                    ╔══════════════════════╗
                                    ║   Orchestrator       ║
                                    ║   Claude Opus 4.7    ║
                                    ╚═══════════╤══════════╝
                                                │  decompose & route
                          ┌─────────────────────┼─────────────────────┐
                          │                     │                     │
                          ▼                     ▼                     ▼
                ┌──────────────────┐  ┌──────────────────┐  ┌──────────────────┐
                │     Planner      │  │   Researcher     │  │     Writer       │
                │  Sonnet 4.6      │  │  Sonnet 4.6      │  │   Sonnet 4.6     │
                ├──────────────────┤  ├──────────────────┤  ├──────────────────┤
                │ Tools:           │  │ Tools:           │  │ Tools:           │
                │  • TodoWrite     │  │  • WebSearch     │  │  • Write         │
                │  • Read          │  │  • WebFetch      │  │  • Edit          │
                │                  │  │  • Read          │  │                  │
                └────────┬─────────┘  └────────┬─────────┘  └────────┬─────────┘
                         │                     │                     │
                         └─────────────────────┼─────────────────────┘
                                               │  return drafts
                                               ▼
                                    ╔══════════════════════╗
                                    ║      Reviewer        ║
                                    ║   Claude Opus 4.7    ║
                                    ╚═══════════╤══════════╝
                                                │  approved
                                                ▼
                                    ┌──────────────────────┐
                                    │   Final response     │
                                    └──────────────────────┘
```

Multi-agent system, drawn end-to-end. Opus coordinators (double-border)
orchestrate Sonnet workers (single-border) each carrying their own tool
list. The shape every modern agent framework converges on.

### Mental model — perception vs reality

```
╔══════════════════════════════════════════════════════════════════════════════════════════════════╗
║                                   HOW AI AGENTS ACTUALLY WORK                                    ║
╚══════════════════════════════════════════════════════════════════════════════════════════════════╝

┌────────────────────────────────────────────────┬─────────────────────────────────────────────────┐
│              PERCEPTION                        │                  REALITY                        │
│                                                │                                                 │
│     Prompt                                     │     Prompt                                      │
│       ▼                                        │       ▼                                         │
│     ✨  Magic  ✨                                │     Parse intent + tokens                       │
│       ▼                                        │       ▼                                         │
│     Answer                                     │     Retrieve context  (RAG, memory)             │
│                                                │       ▼                                         │
│                                                │     Plan  (chain-of-thought, tasks)             │
│                                                │       ▼                                         │
│                                                │     Call tools  (web, code, MCP)                │
│                                                │       ▼                                         │
│                                                │     Verify  (self-check, retry on fail)         │
│                                                │       ▼                                         │
│                                                │     Format answer  +  cite sources              │
│                                                │                                                 │
└────────────────────────────────────────────────┴─────────────────────────────────────────────────┘
   Every invisible step is where the model is actually earning its keep — and where it can fail.
```

The visual asymmetry *is* the insight: 3 boxes vs 7 boxes makes the gap
between mental model and machinery legible at a glance. Same shape works
for "how startups grow," "how compounding works," "how learning happens."

### Before / after — booking sponsorships with SponsorCal

```
╔══════════════════════════════════════════════════════════════════════════════════════════════════╗
║                        BOOKING SPONSORSHIPS — WITHOUT vs WITH SPONSORCAL                         ║
╚══════════════════════════════════════════════════════════════════════════════════════════════════╝

┌────────────────────────────────────────────────┬─────────────────────────────────────────────────┐
│  ✗  WITHOUT SponsorCal                         │  ✓  WITH SponsorCal                             │
│                                                │                                                 │
│  ·  Email threads with 8 sponsors at once      │  ·  One public booking page per creator         │
│  ·  Manual back-and-forth on dates             │  ·  Sponsors self-serve into open slots         │
│  ·  Chase invoices, late payments              │  ·  Stripe checkout: pay first or no slot       │
│  ·  "Are we still on for next week?"           │  ·  Auto reminders 7 / 3 / 1 day before         │
│  ·  Sponsor ghosts, slot wasted                │  ·  10-min reservation lock at checkout         │
│  ·  No data on what works                      │  ·  Per-creator sponsor performance log         │
│                                                │                                                 │
└────────────────────────────────────────────────┴─────────────────────────────────────────────────┘
          From "is sponsorship even worth the chase?" → predictable, recurring revenue.
```

Product storytelling in one screen. Drop into a landing page, a pitch
deck, a Twitter post. The before/after shape is reusable: with vs without
your tool, old way vs new way, status quo vs ambition.

### Cold outbound — bad vs good

```
╔══════════════════════════════════════════════════════════════════════════════════════════════════╗
║                                   COLD OUTBOUND — BAD vs GOOD                                    ║
╚══════════════════════════════════════════════════════════════════════════════════════════════════╝

┌────────────────────────────────────────────────┬─────────────────────────────────────────────────┐
│  ✗  BAD                                        │  ✓  GOOD                                        │
│                                                │                                                 │
│  Subject:                                      │  Subject:                                       │
│     "Quick question"                           │     "Your idempotency post — 1 idea"            │
│                                                │                                                 │
│  Opener:                                       │  Opener:                                        │
│     "Hi {first_name}, hope you're well!"       │     "Saw your retries-vs-locks thread — the bit │
│                                                │      about poison tokens landed."               │
│  Body:                                         │                                                 │
│     "We help companies like yours scale..."    │  Body:                                          │
│                                                │     "We hit the same wall — solved it in 30     │
│  Close:                                        │      lines. Worth showing you?"                 │
│     "Got 15 min on Thursday?"                  │                                                 │
│                                                │  Close:                                         │
│  Outcome:                                      │     "If not relevant, no reply needed."         │
│     Ignored.                                   │                                                 │
│                                                │  Outcome:                                       │
│                                                │     Reply in 3 hours. Call booked.              │
│                                                │                                                 │
└────────────────────────────────────────────────┴─────────────────────────────────────────────────┘
              Cold outreach is not a volume game. It is the work of earning ONE reply.
```

Parallel-structure teaching. Each row anchors a concept (Subject, Opener,
Body, Close, Outcome) so the reader's eye reads sideways for contrast. The
template behind every "how to write a good X" post.

### SQL cheat sheet

```
╔══════════════════════════════════════════════════════════════════════════════════════════════════╗
║                                         SQL CHEAT SHEET                                          ║
╚══════════════════════════════════════════════════════════════════════════════════════════════════╝

┌────────────────────────────────┬────────────────────────────────┬────────────────────────────────┐
│  SELECT                        │  JOIN                          │  AGGREGATE                     │
│  ──────                        │  ────                          │  ─────────                     │
│  SELECT * FROM users;          │  INNER  → rows in both         │  COUNT(*)                      │
│  SELECT name FROM users;       │  LEFT   → all left + matches   │  SUM(amount)                   │
│  SELECT DISTINCT plan FROM …;  │  RIGHT  → all right + matches  │  AVG(price)                    │
│  SELECT name AS n FROM …;      │  FULL   → all rows, both sides │  MIN  /  MAX                   │
│                                │  CROSS  → cartesian product    │  GROUP BY column               │
│  WHERE                         │                                │  HAVING <agg condition>        │
│  ─────                         │  Example:                      │                                │
│  WHERE active = TRUE           │    SELECT u.name, o.total      │  WINDOW                        │
│  AND  /  OR  /  NOT            │    FROM users u                │  ──────                        │
│  IN (1, 2, 3)                  │    JOIN orders o               │  ROW_NUMBER() OVER (…)         │
│  BETWEEN x AND y               │      ON o.user_id = u.id       │  RANK() OVER (PARTITION BY …)  │
│  LIKE 'foo%'   /   ILIKE       │                                │  LAG()  /  LEAD()              │
│  IS NULL  /  IS NOT NULL       │  ORDER & LIMIT                 │  SUM(x) OVER (ORDER BY …)      │
│                                │  ─────────────                 │                                │
│                                │  ORDER BY created DESC         │                                │
│                                │  LIMIT 10 OFFSET 20            │                                │
└────────────────────────────────┴────────────────────────────────┴────────────────────────────────┘
             Read top-to-bottom in each column · combine across columns for full queries
```

Dense, scannable, instantly useful — the format people bookmark. Same
shape works for git commands, regex, vim, kubectl, anything reference-y.

### CV / résumé

```
╔══════════════════════════════════════════════════════════════════════════════════════════════════╗
║                             ALEX RIVERA  ·  Senior Software Engineer                             ║
║                    San Francisco  ·  alex@example.com  ·  github.com/arivera                     ║
╚══════════════════════════════════════════════════════════════════════════════════════════════════╝

┌──────────────────────────────────────────────────────────────────────────────────────────────────┐
│  ABOUT                                                                                           │
│                                                                                                  │
│  Ten years building backend systems for fintech and developer tools. Specialised in              │
│  payment infrastructure, queues, and distributed databases. Currently leading platform           │
│  at Acme Corp. Mentors at Bridge Fellowship on weekends.                                         │
│                                                                                                  │
└──────────────────────────────────────────────────────────────────────────────────────────────────┘

┌────────────────────────────────────────────────┬─────────────────────────────────────────────────┐
│  EXPERIENCE                                    │  STACK                                          │
│                                                │                                                 │
│  Acme Corp     Staff Engineer    2023 — now    │  Languages     Go · TS · Python · Rust          │
│  Stripe        Senior Engineer   2019 — 2023   │  Databases     Postgres · Redis · DynamoDB      │
│  Shopify       Backend Engineer  2017 — 2019   │  Infra         AWS · Kubernetes · Terraform     │
│  Pivotal       Software Engineer 2015 — 2017   │  Observability Datadog · OpenTelemetry          │
│                                                │                                                 │
└────────────────────────────────────────────────┴─────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────────────────────────────────────────────┐
│  SELECT WORK                                                                                     │
│                                                                                                  │
│  •  Designed Stripe's idempotency layer  (2B+ requests/day at < 1 ms p99)                        │
│  •  Led Shopify's queue migration from RabbitMQ to Kafka — 4× throughput, 1/3 cost               │
│  •  Open source: dbmate (3.4k ★) · pg_consul (900 ★) · tdd-quickref (handbook)                   │
│  •  Conference talks: GopherCon 2022, StaffPlus NYC 2024, KubeCon EU 2025                        │
│                                                                                                  │
└──────────────────────────────────────────────────────────────────────────────────────────────────┘
```

Header bar over stacked sections, with a two-column experience + stack
split. Drops cleanly into a GitHub profile README, an email signature, or
a plain-text portfolio.

### Comic (2 panels of 4)

```
┌── Panel 1: At the language exchange ────────────────────────────────────────────────────────────┐
│                                                                                                 │
│   Sofía                                                                Carlos                   │
│   (•‿•)                                                                [•‿•]                    │
│   "¡Hola! ¿Cuántos años tienes?"                                       "¡Hola!"                 │
│                                                                                                 │
└─────────────────────────────────────────────────────────────────────────────────────────────────┘

┌── Panel 2: The mistake ─────────────────────────────────────────────────────────────────────────┐
│                                                                                                 │
│   Sofía                                                                Carlos                   │
│   (¬_¬)                                                                [•_•]                    │
│                                                                       "Yo soy 30 años."         │
│                                                                                                 │
└─────────────────────────────────────────────────────────────────────────────────────────────────┘
```

Character grammar uses brackets for identity: `(face)` round = female, `[face]`
square = male. The full 4-panel arc with stick figures, speech bubbles, and a
narrated takeaway is in `examples/comic-example.md`.

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
