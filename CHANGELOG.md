# Changelog

All notable changes to the skill are documented here.
This project follows [Semantic Versioning](https://semver.org/) loosely:
the version reflects how much the *behavior* of the skill changes.

## [Unreleased]

### Changed

- Rebuilt `understand` around concise, flexible response guardrails.
- Added visual guidance and preserved agent ownership of work.
- Updated Codex metadata and cross-agent installation instructions.
- Removed the unused technique reference.

## [0.1.0] — 2026-06-02

First public release as a standalone repository.

### Added
- `SKILL.md`: three operating modes (Teach or Explain, Reshape an Existing
  Answer, Research or Document), a 10-step comprehension pass, gated additions,
  an output-shape scaffold, and an anti-pattern list.
- `references/technique-reference.md`: the evidence layer — 17 techniques across
  three tiers (Comprehension Core, Teaching Moves, Communication Controls), each
  with rule, rationale, and a before→after, plus the full anti-pattern catalog
  and research anchors.
- `agents/openai.yaml`: Codex UI metadata.
- README with origin story, before→after example, and install instructions for
  Claude Code and Codex.
- MIT license, contributing guide.

[Unreleased]: https://github.com/jkjackson2000/understand/compare/v0.1.0...HEAD
[0.1.0]: https://github.com/jkjackson2000/understand/releases/tag/v0.1.0
