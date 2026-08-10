# CogniTree Skill – Basic Integration Guide

This guide explains how to add the CogniTree Skill to a typical AI agent setup with minimal effort.

---

## 0. Create the `.cognitree/` folder in your project

In the project where your agent works, create:

```text
.cognitree/
  active.md        (can start empty)
  long-term.md     (can start empty)
  episodic/
  latent/
```

CogniTree does not create these files for you; it defines how they should be used.

Your agent or tooling is responsible for writing and reading them.

---

## 1. Install the skill files

Clone the repository:

```bash
git clone https://github.com/pedrocvaranda/cognitree-agent-skill.git
cd cognitree-agent-skill
```

Then copy the `cognitree` skill folder into the appropriate skills directory for your environment:

- **Claude Code / Kimi Code**

  - Personal skills:

    ```text
    ~/.claude/skills/cognitree/
    ```

  - Project skills (inside your repo):

    ```text
    .claude/skills/cognitree/
    ```

- **Cursor / GitHub Copilot-style tooling**

  - Keep the skill under:

    ```text
    .github/skills/cognitree/
    ```

- **Other frameworks**

  - Point your skill loader to the `cognitree` folder and load `SKILL.md` as a system/skill document.

Resulting structure inside your project might look like:

```text
.claude/skills/cognitree/
  SKILL.md
  prompts/
  guides/
  examples/
```

---

## 2. Understand the core pieces

CogniTree consists of:

- `SKILL.md`  
  Main behavioral contract:
  - context optimization,
  - memory model,
  - drift control,
  - `.cognitree/` file contract.

- `prompts/context-optimizer.md`  
  Builds a compact **context pack** from noisy history.

- `prompts/memory-hierarchy.md`  
  Classifies information into:
  - active,
  - episodic,
  - long-term,
  - latent.

- `prompts/drift-detector.md`  
  Detects scope drift and produces alignment notes.

You can use these prompts:

- implicitly, via the skill system (when `when_to_use` matches),  
- or explicitly, by invoking them as sub-skills/tools in your agent.

---

## 3. Minimal usage pattern

A minimal integration looks like this:

1. **Start of a complex task**

   - Use **Context Optimizer** to build a context pack from history:
     - objectives,
     - constraints,
     - key facts and decisions,
     - references,
     - risks and ambiguities,
     - next step suggestion.

   - Store the pack in `.cognitree/active.md` if your environment supports files.

2. **As the conversation grows**

   - Periodically use **Memory Hierarchy** to:
     - keep `.cognitree/active.md` small and high-signal,
     - move older details into episodic or latent memory,
     - promote stable rules into `long-term.md`.

3. **On long or ambiguous workflows**

   - Use **Drift Detector** to:
     - check if current work still matches the original goals,
     - produce an alignment note,
     - ask the user to confirm before major changes in direction.

Even if you do this manually (invoking prompts yourself), you already get most of CogniTree’s benefits.

---

## 4. No library required

CogniTree Skill is **prompt-only**:

- It works purely through SKILL.md and the prompt modules.
- You do not need a separate code library to start using it.
- If you later adopt a CogniTree library or backend, it can implement:
  - `.cognitree/` file handling,
  - snapshots,
  - additional automation.

The skill remains the behavioral specification that explains how to use those structures.

---

## 5. Next steps

After basic integration, consider:

- reading `guides/integration-advanced.md` for:
  - event-driven triggers,
  - meta-agent setups,
  - monitoring and observability;

- adding real-world examples in your own repos inspired by:
  - `examples/chatbot.md`,
  - `examples/research-agent.md`,
  - `examples/coding-agent.md`.
