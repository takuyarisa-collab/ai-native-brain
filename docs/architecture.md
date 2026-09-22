# Architecture

## Goal

ai-native-brain treats long-term context as an external, versioned system rather than as something that must live inside a single chat, model, or vendor.

The architecture has three concerns:

1. **Knowledge** — what has been learned or decided.
2. **Navigation** — how the right context is found without loading everything.
3. **Continuity** — how future sessions can inherit enough of the past to continue coherently.

## Knowledge layers

```text
Raw conversation / work
          │
          ├── project-specific facts ──→ Project source of truth
          │
          └── cross-cutting insight
                    ↓
                  Seed
                    ↓
            repeated observation
                    ↓
          ┌─────────┴─────────┐
          ↓                   ↓
      Principle            Decision
```

### Principle

A relatively stable rule used across situations.

A principle should change slowly. When it changes, the reason for the change should be preserved.

### Decision

A context-specific choice with rationale.

A decision is not universal truth. It records what was chosen under a particular set of constraints.

### Seed

A hypothesis, recurring observation, or unfinished idea.

Seeds are intentionally cheap to create. Most do not need to become projects.

### Project

A stable navigation page for one activity or product area.

A project entry should point to more volatile sources rather than duplicating them.

## Navigation before retrieval

The preferred read path is progressive:

```text
stable entry point
      ↓
short metadata / summary
      ↓
relevant document
      ↓
supporting history only if needed
```

The system should not require every agent to ingest the entire repository.

This allows the same store to remain useful as it grows.

## Source of truth

Markdown files are the durable layer.

Search indexes, embeddings, databases, and caches may be added, but they should be rebuildable from the human-readable store whenever practical.

This makes the memory:

- portable across models,
- inspectable by humans,
- compatible with Git,
- resilient to tool changes.

## Multi-agent use

Different agents can have different roles while sharing the same durable context.

A generic example:

```text
Human
  ↓
Reasoning / planning agent
  ├─ research agent
  ├─ coding agent
  └─ workflow agent
         ↓
      Git / Markdown
      shared memory
```

The shared store does not require every agent to read everything.

Each agent should begin from a role-specific entry point and follow links only as needed.

## Memory lifecycle

A useful lifecycle for uncertain knowledge:

```text
seed
  ↓
growing
  ├─→ principle
  ├─→ decision
  └─→ dormant
```

The purpose is to avoid two common failures:

- forgetting useful unfinished thoughts,
- turning every unfinished thought into a permanent rule.

## Evolution

The architecture is expected to evolve.

New mechanisms should be evaluated by whether they improve one of these:

- retrieval quality,
- continuity,
- provenance,
- maintenance cost,
- human inspectability,
- cross-agent portability.

Complexity is not automatically an improvement.
