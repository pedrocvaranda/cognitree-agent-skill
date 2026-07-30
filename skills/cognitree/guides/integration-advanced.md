# CogniTree Skill – Advanced Integration Guide

This guide covers more advanced ways to integrate the CogniTree Skill with agent frameworks and custom pipelines.

## 1. Treat CogniTree as a meta-agent

You can model CogniTree as a meta-agent responsible for context curation, memory management, and drift detection.

## 2. Event-driven triggers

- Context Optimizer: when context grows large.
- Memory Hierarchy: after major milestones or session end.
- Drift Detector: when scope changes or divergence is suspected.

## 3. Using CogniTree with a library

If you integrate a CogniTree library:
- active memory can map to in-memory buffers,
- episodic memory to session storage,
- long-term memory to persistent storage,
- latent memory to archive storage.

## 4. Interacting with other skills

CogniTree is domain-agnostic and should coexist with other skills.

## 5. Monitoring and observability

Track context pack size, drift frequency, and memory reorganization events to tune the system.
