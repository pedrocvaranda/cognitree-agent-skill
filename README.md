# CogniTree Skill

**Context and memory optimization for AI agents**

[![Status](https://img.shields.io/badge/status-active-success.svg)]()
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![Skill](https://img.shields.io/badge/agent%20skill-portable-blue.svg)]()
[![Framework](https://img.shields.io/badge/framework-agnostic-purple.svg)]()

---

## What is This?

CogniTree Skill is a portable agent skill for improving long-context behavior in AI assistants.

It helps agents answer a practical question:

**“How do we keep an AI agent coherent, focused, and useful across long workflows?”**

**Key Features:**

- **Context optimization** — compress long histories into high-signal context packs  
- **Memory hierarchy** — separate active, episodic, long-term, and latent memory  
- **Drift detection** — catch scope creep and misalignment early  
- **File-based memory contract** — defines how agents should use `.cognitree/active.md`, `episodic/`, `long-term.md`, and `latent/` in the user’s project workspace  
- **Progressive disclosure** — keep core instructions in `SKILL.md` and details in supporting files  
- **Reusable prompts** — specialized prompt modules for different agent behaviors  
- **Framework-agnostic design** — usable in Claude Code, Kimi Code, Cursor, OpenCode, and custom agent stacks  
- **Prompt-only core** — works even without a separate library

---

## Quick Start

### Requirements

- Any AI agent framework that supports SKILL.md-style instruction loading

### Installation

```bash
git clone https://github.com/pedrocvaranda/cognitree-agent-skill.git
cd cognitree-agent-skill
```

### Use in Your Agent

#### Claude Code / Kimi Code

Copy the `cognitree` skill folder into your Claude skills directory:

- Personal skills:

```text
~/.claude/skills/cognitree/
```

- Project skills (inside your repo):

```text
.claude/skills/cognitree/
```

Resulting structure:

```text
.claude/skills/cognitree/
  SKILL.md
  prompts/
  guides/
  examples/
```

Claude Code will then be able to load the skill according to its `SKILL.md` frontmatter and `when_to_use` conditions.

#### Cursor / GitHub Copilot agent-skills-style tooling

Keep the skill under `.github/skills/`:

```text
.github/skills/cognitree/
```

This layout is compatible with tools that scan `.github/skills` to discover installed skills and bundle them.

#### Other frameworks

For other agent frameworks:

- Point the skill loader at the `cognitree` folder.  
- Load `SKILL.md` as a system/skill document.  
- Optionally expose the `prompts/` files as sub-skills or tools.

---

## Usage Overview

How you invoke CogniTree depends on your environment.

- **Automatic:** in environments that understand SKILL.md frontmatter, CogniTree can be considered automatically when `when_to_use` conditions match (long conversations, multi-step tasks, noisy context).  
- **Manual:** you can also trigger the skill explicitly, for example by:
  - running a `/cognitree` or equivalent custom command in your editor, or  
  - including the contents of one of the prompts (e.g. `prompts/context-optimizer.md`) as a system message before a complex step.

Typical workflow:

1. At the start of a complex task, invoke **Context Optimizer** to build a context pack.  
2. Periodically, invoke **Memory Hierarchy** to keep active memory small and organized.  
3. On long or ambiguous workflows, invoke **Drift Detector** to check alignment and write an alignment note.

The guides under `guides/` show concrete patterns for basic and advanced setups.

---

## Files to Load

At minimum:

- `SKILL.md` — main behavioral contract  
- `prompts/context-optimizer.md` — context packing mode  
- `prompts/memory-hierarchy.md` — memory layout mode  
- `prompts/drift-detector.md` — alignment mode  

Recommended support files:

- `guides/integration-basic.md` — minimal integration patterns  
- `guides/integration-advanced.md` — event-driven triggers, multi-agent setups  
- `examples/chatbot.md`  
- `examples/research-agent.md`  
- `examples/coding-agent.md`

---

## What Does It Do?

CogniTree Skill teaches an agent to:

- read history more intelligently,  
- preserve important constraints and preferences,  
- summarize what actually matters,  
- avoid repetitive reprocessing,  
- notice when it is drifting away from the user’s goal,  
- and keep a clear memory structure over time.

It does not replace the agent’s reasoning.  
It improves how the agent manages **attention** over long workflows.

---

## Memory Model and File Layout

CogniTree implements a four-layer memory model:

- **Active memory** — immediate objectives and the current working set.  
- **Episodic memory** — recent steps, intermediate results, and session history.  
- **Long-term memory** — stable rules, specs, and reusable knowledge.  
- **Latent memory** — archived material, old branches, and low-priority history.

To make this real, CogniTree uses a simple file-based contract in the **user’s project workspace**:

```text
.cognitree/
  active.md
  long-term.md
  episodic/
    <session-or-phase>.md
  latent/
    <archive-files>.md
```

These paths refer to files and folders created next to the user’s project files, *not* to files inside this repository.

Agents and coding environments that adopt CogniTree are expected to create and maintain this `.cognitree/` directory when the skill is in use.

- `active.md` — current objective, constraints, latest context pack, last alignment note.  
- `episodic/` — one file per session or phase, capturing what happened in a compact form.  
- `long-term.md` — stable decisions, rules, and specs that should persist.  
- `latent/` — archived logs and deprecated branches for audit/debugging.

The prompts:

- **Context Optimizer** — writes a compact context pack into `active.md`.  
- **Memory Hierarchy** — moves information between `active.md`, `episodic/`, `long-term.md`, and `latent/`.  
- **Drift Detector** — writes alignment notes into `active.md` and relevant episodic files.

> Note: CogniTree does not manipulate these files by itself.  
> The skill defines *what* should be stored and *where*.  
> Your agent or coding environment applies these instructions using its own filesystem or storage layer.

---

## Relation to Built-in Compaction

CogniTree does **not** replace built-in context compaction (such as Claude Code’s auto-compaction).

- Compaction is **reactive** and fires when context is exhausted.  
- CogniTree is **proactive** and in-session.

The intended framing is:

> Use CogniTree to maintain memory hierarchy discipline during long sessions.  
> Let auto-compaction act as the safety net when context runs out.

This positions CogniTree as a complement to, not a competitor of, existing context management features.

---

## Project Structure

```text
cognitree-agent-skill/
  .github/skills/cognitree/
    SKILL.md
    prompts/
      context-optimizer.md
      memory-hierarchy.md
      drift-detector.md
    guides/
      integration-basic.md
      integration-advanced.md
    examples/
      chatbot.md
      research-agent.md
      coding-agent.md
  README.md
  LICENSE
  CONTRIBUTING.md
  CHANGELOG.md
```

---

## Documentation

- [Basic Integration](.github/skills/cognitree/guides/integration-basic.md)  
- [Advanced Integration](.github/skills/cognitree/guides/integration-advanced.md)  
- [Context Optimizer](.github/skills/cognitree/prompts/context-optimizer.md)  
- [Memory Hierarchy](.github/skills/cognitree/prompts/memory-hierarchy.md)  
- [Drift Detector](.github/skills/cognitree/prompts/drift-detector.md)

---

## Evaluation

CogniTree claims to reduce token waste and improve long-term coherence.  
To make these claims measurable, we use a simple evaluation pattern inspired by long-context recall tests:

1. **Plant constraints early**  
   - e.g. “The API key must never be logged”, “We decided against Postgres”, “Use USD, not EUR”.

2. **Bury them under noise**  
   - Run a long, multi-step workflow: discussion, planning, coding, refactors, or research.

3. **Ask constraint-dependent questions at the end**  
   - e.g. “Which database are we using?”, “What currency should prices be shown in?”, “How are secrets handled?”.

4. **Score constraint recall**  
   - Score = fraction of planted constraints that are correctly honoured at the end.  
   - This directly measures long-context memory and alignment.

5. **Compare against a real baseline**  
   - Baseline: the same agent with built-in auto-compaction only (no CogniTree).  
   - Measure:
     - constraint recall,  
     - total tokens used for the full workflow (not just peak context size).

We plan to publish example evaluation scripts and transcripts in a future `eval/` directory.  
In the meantime, you can implement this pattern in your own environment to test CogniTree against your baseline.

---

## Why This Exists

Modern AI agents are smart, but the systems around them often:

- waste tokens,  
- lose important context,  
- drift across long workflows,  
- and struggle to respect earlier decisions and constraints.

CogniTree exists to make long-running agent work feel:

- more coherent,  
- more efficient,  
- and more reliable.

---

## About the Author

**Pedro Coutinho Varanda**

- **#1 Brazil** — National Astronomy Olympiad (OBA 2025, Perfect Score)  
- **#2 Brazil** — OBA 2023  
- **#3 Brazil** — OBA 2024  
- **3× Selected** — International Olympiad on Astronomy and Astrophysics (IOAA)  
- **4× Gold** — Canguru Mathematics Competition (2022–2025)

ML/AI enthusiast | Rio de Janeiro, Brazil  

[GitHub](https://github.com/pedrocvaranda) • [ORCID](https://orcid.org/0009-0004-5199-1745) • [Email](mailto:pedrocvaranda@gmail.com)

---

## Contributing

Contributions are welcome. See [CONTRIBUTING.md](CONTRIBUTING.md) for local setup and guidelines.

Suggested contribution areas:

- Improved prompt wording and robustness.  
- Additional real-world examples for specific tools or frameworks.  
- Integration notes for new agent frameworks.  
- Evaluation scenarios and scripts for long-context behavior.

---

## License

MIT. See [LICENSE](LICENSE).

---

## Status

Active development.
