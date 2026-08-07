# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Semantic Versioning](https://semver.org/).

---

## [1.0.1] – 2026-08-07

### Added

- Enriched `SKILL.md` frontmatter with:
  - `when_to_use`,
  - compatibility metadata,
  - version and author info.
- Defined a concrete `.cognitree/` file-based memory contract:
  - `active.md`,
  - `episodic/`,
  - `long-term.md`,
  - `latent/`.
- Documented promotion/demotion rules between memory layers.
- Clarified the relationship between prompts and `.cognitree/` files.
- Added `guides/integration-basic.md` and updated `guides/integration-advanced.md` with:
  - meta-agent patterns,
  - event-driven triggers,
  - file contract usage.
- Updated `README.md` with:
  - per-framework install paths,
  - relation to built-in auto-compaction,
  - evaluation pattern for long-context behavior,
  - project structure, badges, and author section.
- Added `CONTRIBUTING.md` with contribution guidelines.

### Changed

- Standardized prompt file names to kebab-case:
  - `context-optimizer.md`,
  - `memory-hierarchy.md`,
  - `drift-detector.md`.
- Updated all internal links (README, SKILL.md, guides) to use kebab-case prompt names.
- Updated `prompts/memory-hierarchy.md` to explicitly reference the `.cognitree/` file contract described in `SKILL.md`.

---

## [1.0.0] – 2026-08-06

### Added

- Initial public release of CogniTree Skill.
- Core behavior defined in `SKILL.md`:
  - context optimization,
  - memory hierarchy,
  - drift detection.
- Prompt modules:
  - `context-optimizer`,
  - `memory-hierarchy`,
  - `drift-detector`.
- Basic and advanced integration guides.
- Chatbot, research agent, and coding agent examples.
