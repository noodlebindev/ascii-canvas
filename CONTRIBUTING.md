# Contributing

Thanks for thinking about contributing — this skill is better because of it.

## Quick links

- [Code of Conduct](CODE_OF_CONDUCT.md)
- [Security policy](SECURITY.md)
- [Issue tracker](../../issues)

## Ways to contribute

- **Try the skill and report what breaks.** The most useful contribution is a
  bug report with the exact prompt you used, the skill's output, and what you
  expected instead. File it as a bug-report issue.
- **Improve the SKILL.md instructions or a format file.** Small clarifications,
  fixed typos, better examples — open a PR.
- **Add a new format.** Follow the brainstorm → spec → plan → execute flow used
  for `comic` and `flashcards` (specs in `docs/`). Each format needs: a file
  under `formats/`, an example under `examples/`, an entry in
  `composition-rules/width-budgets.md`, optionally a narrative arc in
  `composition-rules/narrative-arcs.md`, and routing wiring in `SKILL.md`.
- **Add example artefacts.** Real-world examples in `examples/` help others
  see how a format works at full fidelity.
- **Suggest new behaviour.** Open a feature-request issue and propose the
  change before writing a PR — for behavioural changes I prefer to align on
  the approach first.

## Development setup

This is a Claude Code skill — a markdown bundle, no code or build step. To
work on it locally:

```bash
# Clone the repo
git clone <repo-url>
cd ascii-canvas

# Symlink (or copy) into your Claude skills directory
ln -s "$(pwd)" ~/.claude/skills/ascii-canvas
```

Then in Claude Code, invoke the skill (`/ascii-canvas make me a flowchart of
how X works`) and iterate on the relevant file.

## Verifying changes

There is no automated test runner. The acceptance loop is:

1. Make your edit.
2. In a fresh Claude Code session with the skill loaded, run the prompt that
   exercises your change.
3. Manually verify the output against the rules in `composition-rules/`.
4. For width-sensitive changes, run the Python width check:
   ```python
   import re
   c = open('formats/<name>.md').read()
   blocks = re.findall(r'```[a-z]*\n(.*?)```', c, re.DOTALL)
   for i, b in enumerate(blocks, 1):
       w = max(len(l) for l in b.split('\n')) if b.strip() else 0
       print(f'block {i}: width {w}')
   ```

## Pull request process

1. Fork the repo and create a branch from `main`.
2. Make your change. Keep PRs focused — one logical change per PR.
3. Update `CHANGELOG.md` under `[Unreleased]`.
4. Open the PR using the template. Link any issue it closes.

## Style

- SKILL.md and format files: clear imperative voice, short paragraphs, explain
  *why* alongside *what*. Avoid heavy MUSTs unless the behaviour is genuinely
  non-negotiable.
- Commit messages: conventional commits (`feat:`, `fix:`, `docs:`, `chore:`)
  preferred. Scope the commit to the affected format where useful:
  `feat(flashcards): ...`.
- Width discipline: every code-fenced block in `formats/` and `examples/` must
  fit the format's declared width budget. The width check command above is the
  authoritative test.

## Code of Conduct

By contributing, you agree to abide by the [Code of Conduct](CODE_OF_CONDUCT.md).
