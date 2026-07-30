# CogniTree Skill – Basic Integration Guide

This guide explains how to add the CogniTree Skill to a typical AI agent setup.

## 1. Add SKILL.md to your agent

- Copy `SKILL.md` into your project or reference this repository.
- Ensure your agent framework loads SKILL.md as part of the system or skill context.

## 2. Decide when to use the prompts

- `context_optimizer.md` for large context compression.
- `memory_hierarchy.md` for memory layout and summarization.
- `drift_detector.md` for alignment checks.

## 3. Minimal integration pattern

1. Build a context pack before a complex step.
2. Reorganize memory after a significant stage.
3. Run drift checks periodically.

## 4. No library required

CogniTree Skill is pure prompt-level.
You do not need any external API or code library to benefit from it.
