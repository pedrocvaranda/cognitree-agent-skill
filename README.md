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

**"How do we keep an AI agent coherent, focused, and useful across long workflows?"**

**Key Features:**

- **Context optimization** — compress long histories into high-signal context packs
- **Memory hierarchy** — separate active, episodic, long-term, and latent memory
- **Drift detection** — catch scope creep and misalignment early
- **Progressive disclosure** — keep core instructions in `SKILL.md` and details in supporting files
- **Reusable prompts** — specialized prompt modules for different agent behaviors
- **Framework-agnostic design** — usable in Claude Code, Cursor, OpenCode, and custom agent stacks
- **Prompt-only core** — works even without a separate library

---

## Quick Start

### Requirements

- Any AI agent framework that supports skill-style instruction loading

### Installation

```bash
git clone https://github.com/your-username/cognitree-agent-skill.git
cd cognitree-agent-skill
```

### Use in Your Agent

Add the skill directory to your agent's skill path:

```text
.github/skills/cognitree/
```

Or copy the `SKILL.md` and supporting files into your agent's configured skills directory.

### Files to Load

- `SKILL.md` — main behavioral contract
- `prompts/context_optimizer.md` — context packing mode
- `prompts/memory_hierarchy.md` — memory layout mode
- `prompts/drift_detector.md` — alignment mode

### Examples

- `examples/chatbot.md`
- `examples/research-agent.md`
- `examples/coding-agent.md`

---

## What Does It Do?

CogniTree Skill teaches an agent to:

- read history more intelligently,
- preserve important constraints,
- summarize what matters,
- avoid repetitive reprocessing,
- and notice when it is drifting away from the user’s goal.

It does not replace the agent’s reasoning.
It improves how the agent manages attention over time.

---

## Project Structure

```text
cognitree-agent-skill/
 .github/skills/cognitree/
 SKILL.md
 prompts/
   context_optimizer.md
   memory_hierarchy.md
   drift_detector.md
 guides/
   integration-basic.md
   integration-advanced.md
 examples/
   chatbot.md
   research-agent.md
   coding-agent.md
 README.md
 LICENSE
```

---

## Documentation

- [Basic Integration](.github/skills/cognitree/guides/integration-basic.md)
- [Advanced Integration](.github/skills/cognitree/guides/integration-advanced.md)
- [Context Optimizer](.github/skills/cognitree/prompts/context_optimizer.md)
- [Memory Hierarchy](.github/skills/cognitree/prompts/memory_hierarchy.md)
- [Drift Detector](.github/skills/cognitree/prompts/drift_detector.md)

---

## Why This Exists

Modern AI agents are smart, but the systems around them often waste tokens, lose context, and drift across long workflows.

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
- **3x Selected** — International Olympiad on Astronomy and Astrophysics (IOAA)
- **4x Gold** — Canguru Mathematics Competition (2022–2025)

ML/AI enthusiast | Rio de Janeiro, Brazil

[GitHub](https://github.com/pedrocvaranda) • [ORCID](https://orcid.org/0009-0004-5199-1745) • [Email](mailto:pedrocvaranda@gmail.com)

---

## Contributing

Contributions are welcome.

Suggested contribution areas:
- better prompt wording,
- more example skills,
- adapters for specific agent frameworks,
- benchmarks and evaluation scripts.

---

## Related Projects

* [Cash Allocation Model](https://github.com/pedrocvaranda/modelo_alocacao_caixa) — Capital allocation system with scenario simulation and ML optimization
* [Varandian Optics Simulator](https://github.com/pedrocvaranda/varadian-optics-simulator) — Light propagation simulator in curved spaces
* [Portfolio Tracker](https://github.com/pedrocvaranda/portfolio-tracker) - Monte Carlo simulation engine for market data collection, price validation, parameter calibration, and forecast backtesting

——-

## License

MIT. See [LICENSE](LICENSE).

---

## Status

Active development.
