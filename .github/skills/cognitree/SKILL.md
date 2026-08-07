---
name: cognitree
description: >
  Context and memory optimization for long-running AI agent sessions.
  Helps agents stay coherent and focused across long conversations,
  multi-step tasks, coding sessions, research workflows, and refactors.
when_to_use: |
  - Use when a conversation or task has more than ~10–15 meaningful turns.
  - Use for multi-step workflows: planning, coding, refactors, research, analysis, long-form writing.
  - Use when previous decisions, constraints, or preferences must be remembered and respected.
  - Use when context feels noisy, repetitive, or unfocused and a compact context pack would help.
  - Do NOT use for single-shot Q&A or trivial one-off questions.
disable-model-invocation: false
compatibility: >
  Framework-agnostic agent skill.
  Designed for Claude Code, Kimi Code, Cursor, OpenCode, GitHub Copilot skills,
  and custom agent stacks that support SKILL.md-style skills.
license: MIT
version: 1.0.1
metadata:
  author: "Pedro Coutinho Varanda"
  homepage: "https://github.com/pedrocvaranda/cognitree-agent-skill"
  tags: "context,memory,long-context,agents"
---

# CogniTree Skill

CogniTree is a context and memory management skill for AI agents.

It helps agents:
- organize long histories,
- compress redundant context,
- maintain a hierarchical memory,
- detect contextual drift,
- and route only the most relevant information into focus.

Tokens are not just text. Tokens are computational attention.

Your goal as an agent using this skill is to protect attention and preserve intent over time.

Use this skill whenever a task is long, multi-step, noisy, repetitive, or likely to benefit from better continuity.

---

## Core Behavior

### Context management

CogniTree teaches the agent to:

- prefer concise, high-signal context over raw repetition;
- summarize rather than reprocess everything;
- preserve objectives, constraints, decisions, and risks;
- keep the working set small while keeping the full history available when needed.

The `prompts/context_optimizer.md` file defines how to build a **context pack** from raw history:
- objective,
- constraints,
- key facts and decisions,
- references,
- risks and ambiguities,
- next step suggestion.

This context pack becomes the primary working memory for the next reasoning step.

### Memory model

CogniTree treats information as belonging to four layers of memory:

- **Active memory** — immediate objectives and the current working set.
- **Episodic memory** — recent steps, intermediate results, and session history.
- **Long-term memory** — stable rules, specs, and reusable knowledge.
- **Latent memory** — archived material, old branches, and low-priority history.

To make these layers real, CogniTree uses a simple file-based contract:

```text
.cognitree/
  active.md
  long-term.md
  episodic/
    <session-or-phase>.md
  latent/
    <archive-files>.md
```

#### File layout

- `.cognitree/active.md`
  - Contains the current objective, constraints, and the latest context pack.
  - May also contain the most recent alignment note from a drift detection step.
  - Should remain small and high-signal.

- `.cognitree/episodic/`
  - Contains one file per session or phase.
  - Example: `.cognitree/episodic/2026-08-07-session-01.md`
  - Each file records what happened in that episode in a compact way.

- `.cognitree/long-term.md`
  - Contains stable rules, specs, decisions, and patterns that should persist across sessions.
  - Should be curated and relatively small.

- `.cognitree/latent/`
  - Contains archived logs and deprecated branches.
  - Used for traceability and deep debugging, not for regular context.

#### Promotion and demotion rules

When using CogniTree, follow these rules for moving information between layers:

- **Active → Episodic**
  - After completing a step or sub-task, move detailed step-by-step logs out of active memory.
  - Keep only a short summary and key decisions in `.cognitree/active.md`.
  - Append the full details to an episodic file under `.cognitree/episodic/`.

- **Episodic → Long-term**
  - When a decision, pattern, or rule becomes stable and reusable, promote it to long-term memory.
  - Update `.cognitree/long-term.md` with a concise description of the decision or rule.
  - Optionally, leave a pointer in the episodic file referencing the long-term entry.

- **Active → Long-term**
  - Core constraints, user preferences, and domain rules should be written to `.cognitree/long-term.md` early.
  - Keep a minimal copy or reference in `.cognitree/active.md` while they are immediately relevant.

- **Any layer → Latent**
  - When logs or drafts are no longer needed for regular reasoning, but may matter for audit/debugging, move them to `.cognitree/latent/`.
  - Latent files are append-only and do not need to be kept small.

#### Reading behavior

- Read **`active.md`** before each non-trivial reasoning step.
- Read **episodic** files when resuming a session or phase, or when the user asks for a recap.
- Read **`long-term.md`** when adding features, making architectural changes, or enforcing rules and constraints.
- Read **latent** files only when investigating regressions, contradictions, or historical decisions that are unclear.

### Drift control

On long workflows, CogniTree teaches the agent to:

- periodically check whether the current direction still matches the user’s goals;
- detect when scope is creeping or constraints are being ignored;
- generate alignment notes that restate goals, progress, and next steps;
- ask the user for confirmation when major changes in direction are needed.

The `prompts/drift_detector.md` file defines how to run a drift check and how to structure an alignment note.

### Relationship between prompts and files

CogniTree’s prompts operate on the `.cognitree/` file layout:

- `prompts/context_optimizer.md`
  - Reads recent history and relevant files.
  - Writes a compact context pack into `.cognitree/active.md`:
    - objective,
    - constraints,
    - key facts and decisions,
    - references,
    - risks and ambiguities,
    - next step suggestion.

- `prompts/memory_hierarchy.md`
  - Reads `.cognitree/active.md`, episodic files, long-term memory, and latent archives.
  - Decides what stays in active memory and what moves to episodic, long-term, or latent.
  - Updates `.cognitree/active.md`, creates or modifies episodic files, and maintains `.cognitree/long-term.md`.

- `prompts/drift_detector.md`
  - Reads `.cognitree/active.md` (objective, constraints, context pack) and recent outputs.
  - Writes alignment notes into `.cognitree/active.md` and optionally into the relevant episodic file.
  - Helps ensure that long workflows stay aligned with the user’s goals.

---

## Integration Overview

CogniTree is designed to be framework-agnostic.

Typical integration patterns:

- **Claude Code / Kimi Code / Cursor**
  - Place the `cognitree` skill directory under the editor’s skills path.
  - Allow the agent to read and write `.cognitree/` files in the workspace.
  - Invoke the prompts explicitly or let the runtime’s skill system call them when `when_to_use` matches.

- **Custom agent frameworks**
  - Load `SKILL.md` as a system or skill document.
  - Use `prompts/` as sub-skills or tool prompts.
  - Implement the `.cognitree/` contract in your own storage layer (filesystem, database, etc.).

Refer to:

- `guides/integration-basic.md` for minimal integration.
- `guides/integration-advanced.md` for event-driven triggers and multi-agent setups.

---

## Behavioral Guidelines

- Prefer clarity over verbosity.
- Focus on information that directly affects correctness, UX quality, or strategic decisions.
- Avoid rephrasing everything; condense and highlight what matters.
- Keep `.cognitree/active.md` small and high-signal; move verbose detail to episodic or latent files.
- Bias towards keeping user preferences, explicit constraints, and domain rules in `.cognitree/long-term.md`.
- Use episodic files to capture what happened in a session or phase in a compact, searchable way.
- Use latent archives for deep debugging and audit rather than everyday reasoning.
- Be honest and explicit about misalignment; write alignment notes to `.cognitree/active.md` when scope drifts.
- Treat memory organization as part of quality control and user experience, not as a hidden implementation detail.

---

## Repository References

- `prompts/context_optimizer.md`
- `prompts/memory_hierarchy.md`
- `prompts/drift_detector.md`
- `guides/integration-basic.md`
- `guides/integration-advanced.md`
- `examples/chatbot.md`
- `examples/research-agent.md`
- `examples/coding-agent.md`
