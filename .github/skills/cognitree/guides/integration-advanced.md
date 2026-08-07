# CogniTree Skill – Advanced Integration Guide

This guide covers more advanced ways to integrate CogniTree Skill with agent frameworks and custom pipelines.

---

## 1. Treat CogniTree as a meta-agent

You can model CogniTree as a dedicated **context manager** agent responsible for:

- context curation,
- memory hierarchy management,
- drift detection and alignment.

In multi-agent frameworks:

- Create a “Context Manager” agent using CogniTree’s `SKILL.md` and prompts.
- Route long-running tasks through this agent before the main domain agents (coding, UX, research, etc.).
- Let the context manager:
  - read raw history and relevant files,
  - update `.cognitree/` files,
  - hand a compact context pack back to the main agent.

---

## 2. File-based memory contract

CogniTree uses a simple file layout to make its memory hierarchy real:

```text
.cognitree/
  active.md
  long-term.md
  episodic/
    <session-or-phase>.md
  latent/
    <archive-files>.md
```

Recommended usage:

- `active.md`
  - Stores the current objective, constraints, latest context pack, and last alignment note.
  - Should remain small and high-signal.

- `episodic/`
  - Stores one file per session or phase, with a compact narrative of what happened.
  - Ideal for resuming work and generating recaps.

- `long-term.md`
  - Stores stable rules, specs, and decisions that should persist across sessions.
  - Should be curated and relatively small.

- `latent/`
  - Stores archived logs and deprecated branches.
  - Used for audit and deep debugging, not everyday context.

When running in a file-based coding environment (Claude Code, Kimi Code, Cursor, etc.), configure your agent so that:

- **Context Optimizer** updates `.cognitree/active.md` with the latest context pack.
- **Memory Hierarchy** moves information between `active.md`, `episodic/`, `long-term.md`, and `latent/`.
- **Drift Detector** writes alignment notes into `active.md` and the relevant episodic file.

---

## 3. Event-driven triggers

Define triggers to decide when each prompt should run.

### Context Optimizer (`prompts/context-optimizer.md`)

Trigger when:

- total message count exceeds a threshold (e.g. 10–15 meaningful turns),
- a new phase of work starts (planning, coding, refactor, research),
- large documents, logs, or specs are added,
- the agent is about to perform a complex, multi-step action.

### Memory Hierarchy (`prompts/memory-hierarchy.md`)

Trigger when:

- a phase or session completes,
- you are about to pause and resume later,
- the `.cognitree/active.md` file grows too large,
- you want to “clean up” the working set while preserving history.

### Drift Detector (`prompts/drift-detector.md`)

Trigger when:

- goals or constraints have changed over time,
- the user expresses confusion or dissatisfaction,
- the agent has gone through many iterations on the same task,
- you suspect scope creep or misalignment.

Implement these triggers using:

- middleware in your agent stack,
- event listeners on message/step counts,
- or simple heuristics based on token usage and file sizes.

---

## 4. Using CogniTree with a library or backend

If you integrate a CogniTree-compatible library or backend:

- Map the four memory layers to storage primitives:

  - Active memory → in-memory buffer + `.cognitree/active.md`.
  - Episodic memory → session store + `.cognitree/episodic/`.
  - Long-term memory → database or knowledge base + `.cognitree/long-term.md`.
  - Latent memory → archive storage + `.cognitree/latent/`.

- Use Context Optimizer outputs as **snapshots**:
  - each context pack can be stored as a versioned state of understanding,
  - use snapshot IDs to resume or compare reasoning later.

- Use Drift Detector alignment notes as:
  - explicit checkpoints in your pipeline,
  - annotations on tasks (objective, progress, next steps).

This allows CogniTree to be both a prompt-level skill and a specification for your memory backend.

---

## 5. Interacting with other skills

CogniTree is domain-agnostic and should coexist with other skills:

- UX / design skills,
- architecture / coding skills,
- business / strategy skills,
- documentation / research skills.

Best practice:

- Let domain skills own the **what** (content, logic, domain expertise).
- Let CogniTree own the **how over time** (context, memory, continuity, drift control).

You can:

- run CogniTree as a pre-processing step (build context pack → call domain skill),
- or as a parallel meta-agent that keeps `.cognitree/` up to date while others work.

---

## 6. Monitoring and observability

Track how CogniTree affects behavior over time.

Suggested metrics:

- size of `.cognitree/active.md` vs. raw history size,
- number and frequency of drift events detected,
- number of memory reorganization events (episodic / long-term / latent updates),
- constraint recall on long workflows (see README “Evaluation” section).

Use these metrics to:

- tune thresholds and triggers,
- justify token cost reductions,
- debug strange agent behaviors,
- and compare against your baseline (built-in compaction only, no CogniTree).

This makes CogniTree not only a UX improvement for users, but also a tool for engineers to understand how context is being used.
