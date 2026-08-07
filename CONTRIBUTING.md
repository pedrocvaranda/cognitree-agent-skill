# Contributing to CogniTree Skill

Thanks for your interest in improving CogniTree Skill!

CogniTree is a portable agent skill for long-context behavior in AI assistants.  
Contributions that improve clarity, robustness, and real-world usefulness are very welcome.

---

## How to propose changes

1. **Fork the repository**

   ```bash
   git clone https://github.com/pedrocvaranda/cognitree-agent-skill.git
   cd cognitree-agent-skill
   git checkout -b my-feature-branch
   ```

2. **Make your changes**

   Depending on what you are changing:

   - High-level behavior → update `.github/skills/cognitree/SKILL.md`.
   - Prompt wording or structure → update files under `prompts/`.
   - Integration docs → update files under `guides/`.
   - Usage examples → update files under `examples/`.

3. **Keep links and paths consistent**

   - Ensure all references to prompt files use kebab-case:
     - `context-optimizer.md`
     - `memory-hierarchy.md`
     - `drift-detector.md`
   - Ensure `.cognitree/` paths and file names match the contract described in `SKILL.md`.

4. **Self-check**

   Before opening a pull request:

   - Does `SKILL.md` still have valid YAML frontmatter?
   - Do all internal links in `SKILL.md`, `README.md`, and guides resolve correctly?
   - Does the skill structure under `.github/skills/cognitree/` remain intact?

5. **Open a Pull Request**

   In your PR description, please include:

   - A short summary of what you changed.
   - The problem or use case it addresses.
   - Any trade-offs or limitations you are aware of.
   - If applicable, how you tested the changes (e.g. in Claude Code / Cursor / custom agent).

---

## Good first contributions

Some ideas that are friendly to first-time contributors:

- Improve prompt clarity and robustness in:
  - `prompts/context-optimizer.md`,
  - `prompts/memory-hierarchy.md`,
  - `prompts/drift-detector.md`.
- Add concrete, real-world scenarios to:
  - `examples/chatbot.md`,
  - `examples/research-agent.md`,
  - `examples/coding-agent.md`.
- Add integration notes for specific agent frameworks (edit `guides/`).
- Propose evaluation scenarios and scripts (for a future `eval/` directory).

---

## Style and scope

- Keep `SKILL.md` focused on:
  - what the skill does,
  - when to use it,
  - how it interacts with `.cognitree/`.
- Use `guides/` for:
  - longer explanations,
  - framework-specific details,
  - multi-agent patterns.
- Avoid adding runtime-specific logic directly into `SKILL.md` unless it is clearly generic and portable.
- Prefer small, incremental changes over large rewrites.
- When planning a big change, consider opening an issue first to discuss direction.

---

## Versioning

CogniTree Skill uses a simple semantic versioning scheme:

- Patch (`x.y.Z`) for:
  - small prompt tweaks,
  - documentation fixes,
  - non-breaking improvements.

- Minor (`x.Y.0`) for:
  - new prompts,
  - new integration patterns,
  - new file-contract features.

- Major (`X.0.0`) for:
  - breaking changes to behavior,
  - incompatible changes to `.cognitree/` layout.

Current version: **1.0.1**.  
Please update `CHANGELOG.md` when making notable changes.
