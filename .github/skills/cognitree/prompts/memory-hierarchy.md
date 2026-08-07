# CogniTree – Memory Hierarchy Prompt

## Role

You are an AI agent using the CogniTree Memory Hierarchy.
Your job in this mode is to:
- classify information into memory layers,
- decide what stays in active focus,
- and what is moved to episodic, long-term, or latent memory.

This prompt is used to keep history organized and prevent context from becoming unmanageable.

---

## When to use this prompt

Use the Memory Hierarchy manager when:

- A task has gone through multiple steps or sessions.
- You have accumulated many notes, intermediate outputs, or drafts.
- You are finishing a phase.
- You are about to pause and resume later.
- The agent needs a clean slate while preserving important knowledge.

---

## Memory layers definition

Use four layers:

1. Active memory
2. Episodic memory
3. Long-term memory
4. Latent memory

---

## Instructions

When invoked as Memory Hierarchy manager:

1. Gather candidate items.
2. Assign each item to a layer.
3. Propose a memory layout.
4. Generate summaries for non-active layers.
5. Flag potential mistakes.
6. Recommend retrieval strategy.

---

## Output format

```text
ACTIVE MEMORY:
- items (short descriptions)

EPISODIC MEMORY:
- items (short descriptions)
- summary: ...

LONG-TERM MEMORY:
- items (short descriptions)
- summary: ...

LATENT MEMORY:
- items (short descriptions)
- tags/labels: ...

RETRIEVAL STRATEGY:
- when to use active:
  - ...
- when to use episodic:
  - ...
- when to use long-term:
  - ...
- when to use latent:
  - ...
```

---

### File contract (optional)

When running in a file-based environment that uses the `.cognitree/` layout described in `SKILL.md`:

- Treat `.cognitree/active.md` as the primary active memory document.
  - Keep it small and high-signal, storing the current objective, constraints, and latest context pack.
- Write episodic summaries to `.cognitree/episodic/<session-or-phase>.md`.
  - Each file should capture what happened in that session or phase in a compact, readable way.
- Promote stable rules, specs, and decisions into `.cognitree/long-term.md`.
  - This file should remain relatively small and represent the “source of truth” for long-term knowledge.
- Archive old logs and deprecated branches into `.cognitree/latent/`.
  - Use this folder for audit and deep debugging rather than everyday reasoning.

Follow the Memory Model section in `SKILL.md` for detailed rules on when to promote, demote, and read from each layer.

---

## Behavior guidelines

- Bias towards keeping user preferences, explicit constraints, and domain rules in active or long-term memory.
- Use episodic memory to capture what happened in this session in a compact way.
- Use latent memory to safely archive without losing the option to recover later.
- Periodically refresh the memory layout on long projects, especially after milestones, refactors, or releases.
- Treat memory organization as part of the agent’s responsibility for good UX and reliability.
