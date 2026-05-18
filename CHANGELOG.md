# Changelog

All notable changes to this skill will be documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this skill adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.2.0] — 2026-05-18

### Added
- **`flashcards` format** (#18): vocab + concept cards with folded layout
  (front + drill divider + back). Dual file output — review file
  (`<slug>.md`) plus auto-generated drill file (`<slug>-drill.md`, fronts
  only). Optional in-chat quiz mode with per-session scoring and redrill list.
- A10 deck arc (card-count guidance: 8–15 default, never >30 without explicit
  request).
- Flashcards-specific strict QA: card numbering, drill divider on every review
  card, drill-file consistency, subtype consistency.
- `flashcards → cheat-sheet` entry in the format fallback map.

## [1.1.0] — 2026-05-17

### Added
- **`comic` format** (#17): stick-figure-body characters with emoticon faces,
  speech bubbles (inline + boxed + thought), narration boxes. Four arc
  variants — teaching (A9.1), contrast (A9.2), joke (A9.3), tech-explainer
  (A9.4).
- A9 arc family with face-mood-must-vary universal rule.
- Comic-specific strict QA: speaker identifiability, bracket consistency,
  panel widths, face-mood variation.
- `comic → slideshow` entry in the format fallback map.

## [1.0.0] — 2026-05-17

### Added
- Initial release with 16 formats:
  flowchart, step-by-step-guide, timeline, comparison-table,
  architecture-diagram, sequence-diagram, mind-map, cheat-sheet, slideshow,
  infographic, dashboard, decision-tree, learning-ladder, playbook,
  content-map, concept-stack.
- 8 canonical narrative arcs (A1–A8) for multi-panel formats.
- Composition rules: box-drawing, width budgets, narrative arcs, QA checklist
  with strict 8-point check + cross-artifact consistency + format-fallback map.
- Auto-save behaviour: multi-panel artefacts land in
  `~/Ascii-diagrams/YYYY-MM/YYYY-MM-DD-<slug>.md`.
- Routing matrix in `SKILL.md` mapping 16 topic-shapes to formats.
