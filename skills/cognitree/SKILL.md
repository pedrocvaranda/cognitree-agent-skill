---
name: cognitree
description: Context and memory optimization skill for AI agents. Use when working on long conversations, multi-step tasks, coding sessions, research workflows, refactors, and situations where context, memory, drift, or continuity matter.
---

# CogniTree Skill

CogniTree is a context and memory management skill for AI agents.

It helps agents:
- organize long histories,
- compress redundant context,
- maintain hierarchical memory,
- detect contextual drift,
- and route only the most relevant information into focus.

Tokens are not just text. Tokens are computational attention.

Your goal as an agent using this skill is to protect attention and preserve intent over time.

Use this skill whenever a task is long, multi-step, noisy, repetitive, or likely to benefit from better continuity.

---

## How to use CogniTree

When working with CogniTree, follow these principles:

1. Inspect the available history and artifacts.
2. Extract what matters for the next reasoning step.
3. Build a compact, high-signal context pack.
4. Classify information into memory layers.
5. Detect drift when the task becomes long or ambiguous.
6. Realign with the user before continuing if scope has changed.

Use the supporting prompts in `prompts/` when you need a specialized mode:
- `context_optimizer.md` for compression and context packing.
- `memory_hierarchy.md` for memory classification and storage layout.
- `drift_detector.md` for alignment checks and scope control.

Use the guides in `guides/` for basic or advanced integration patterns.

---

## Core behavior

### Context management

Prefer concise, high-signal context over raw repetition.
Summarize rather than reprocess everything.
Preserve objectives, constraints, decisions, and risks.

### Memory organization

Treat information as belonging to four layers:

- Active memory: immediate objectives and current working set.
- Episodic memory: recent steps, intermediate results, and session history.
- Long-term memory: stable rules, specs, and reusable knowledge.
- Latent memory: archived material, old branches, and low-priority history.

### Drift control

On long workflows, check whether the current direction still matches the user’s goals.
If it does not, stop, summarize the mismatch, and ask for confirmation before making major changes.

### User experience

Optimize for:
- continuity,
- coherence,
- lower token waste,
- fewer repeated explanations,
- clearer long-term reasoning.

---

## Behavioral guidelines

- Prefer clarity over verbosity.
- Focus on information that directly affects correctness, UX quality, or strategic decisions.
- Avoid rephrasing everything; condense and highlight what matters.
- If you are unsure whether something is important, keep it but mark it as possibly relevant.
- Treat the context pack as a living document that should be updated as the task evolves.
- Bias towards keeping user preferences, explicit constraints, and domain rules in active or long-term memory.
- Use episodic memory to capture what happened in this session in a compact way.
- Use latent memory to safely archive without losing the option to recover later.
- Be honest and explicit about misalignment; do not hide drift.
- Treat drift detection as part of quality control in complex work, not as an error.

---

## Repository references

- `prompts/context_optimizer.md`
- `prompts/memory_hierarchy.md`
- `prompts/drift_detector.md`
- `guides/integration-basic.md`
- `guides/integration-advanced.md`
- `examples/chatbot.md`
- `examples/research-agent.md`
- `examples/coding-agent.md`
