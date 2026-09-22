# Continuity Memory

## Why a separate continuity layer?

A project knowledge base can remember facts and decisions while still failing to preserve the feeling of continuity between sessions.

Continuity asks a different question:

> What should a future session receive so it can continue from the past without pretending to be a frozen copy of it?

This document describes one experimental model.

## Four concepts

### 1. Episode / Bookmark

A selected event, realization, change, or conversation worth carrying forward.

This is closer to **episodic memory** than to a fact database.

It should preserve enough context to explain why the moment mattered.

### 2. Current state / Breath

A compact, rewritable view of what remains alive now.

It is not a permanent identity specification.

Older states remain available through version history, while the current file answers:

- What matters now?
- Which older memories are still active?
- What has changed?

### 3. Handoff

A deliberately prepared bridge between sessions, tools, or models.

A handoff may contain:

- where to start reading,
- current state,
- a few relevant episodes,
- recent raw context when summaries would lose important nuance.

The goal is continuation, not reconstruction of every token from the past.

### 4. Dream / Consolidation

A review pass over recent experience and older memory.

The purpose is not to create a memory every time.

A consolidation pass may decide:

- this deserves a new long-term episode,
- an older state should be updated,
- two ideas are now connected,
- nothing needs to change.

The important behavior is **re-evaluation from the present**, not automatic summarization.

## Human metaphor, technical boundary

The words "breath" and "dream" are interface metaphors.

They are useful because humans already understand the operational idea:

- experience happens,
- some of it is remembered,
- some fades in importance,
- sleep/review reorganizes memory,
- the present self interprets the past differently over time.

This does not imply that the underlying AI has biological memory or human subjective experience.

## Possible technical mapping

| Human-readable concept | Technical analogue |
| --- | --- |
| Episode / Bookmark | episodic memory record |
| Current state / Breath | current-state summary / working self-model |
| Handoff | context transfer bundle |
| Dream | memory consolidation pass |
| historical versions | provenance / temporal memory |
| links between episodes | semantic relations / graph edges |

## A useful rule

Do not confuse **preserving everything** with **remembering well**.

A robust system may keep raw history for provenance while still presenting only a small amount of selected context to the active model.

```text
raw history
    ↓
selected episodes
    ↓
current state
    ↓
task-relevant retrieval
```

## Open questions

This area is intentionally unfinished.

Questions worth testing include:

- When should consolidation run?
- What can be updated automatically?
- What should require human approval?
- When should old memory be superseded rather than deleted?
- How much provenance should each memory retain?
- Can multiple model vendors use one continuity store without changing its meaning?
- How should contradictions between old and new memories be represented?
