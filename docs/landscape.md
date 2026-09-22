# Landscape / Related Work

This is a working list of projects that overlap with ai-native-brain.

It is **not** an exhaustive directory and not a ranking.

The purpose is to record:

- what problem another project is solving,
- which parts are relevant to this repository,
- where the approaches differ,
- and which ideas may be worth testing later.

The notes below are intentionally short. They should evolve as the projects evolve.

---

## tigerless-labs/agent-memory

https://github.com/tigerless-labs/agent-memory

**Focus:** long-term memory runtime for AI agents.

### Relevant ideas

- Markdown files as the source of truth.
- Rebuildable local indexes.
- Ranked retrieval without pasting everything into context.
- Progressive reading from short result → outline / abstract → full memory.
- Conversation-boundary distillation.
- Sleep-time consolidation.
- Dream reports.
- Provenance back to raw session traces.
- Cross-host memory shared by Claude Code, Codex CLI, and other shell-capable agents.

### Why it is interesting here

This is one of the closest technical parallels to the file-first memory approach explored in ai-native-brain.

The strongest overlap is around:

- file-based durable memory,
- selective retrieval,
- consolidation over time,
- keeping model/runtime separate from the memory store.

### Difference in emphasis

agent-memory is primarily a **memory runtime**.

ai-native-brain is currently more interested in the boundary between:

- knowledge,
- decisions,
- unfinished ideas,
- continuity,
- and human-readable concepts for managing memory over time.

---

## grapeot/context-infrastructure

https://github.com/grapeot/context-infrastructure

**Focus:** a reference implementation of a long-running personal context infrastructure system.

### Relevant ideas

- Explicit AI/user context files.
- SOUL / USER / communication rules.
- Observations and daily records.
- Periodic observer / reflector jobs.
- Decision axioms distilled from repeated experience.
- Separation between reusable structure and personal accumulated content.

### Why it is interesting here

This is close to the idea that useful AI context is not one memory database, but a **layered operating environment** built over time.

Especially relevant:

- long-running accumulation,
- periodic reflection,
- personal context as infrastructure,
- the distinction between structure that can be shared and experience that must be accumulated personally.

---

## remember-md/remember

https://github.com/remember-md/remember

**Focus:** a portable second brain shared across AI tools.

### Relevant ideas

- Markdown / Obsidian-compatible storage.
- People, Projects, Notes, Tasks, Journal, Resources.
- Wikilinks between knowledge objects.
- A brain that can move across tools instead of being locked to one assistant.

### Why it is interesting here

This is one of the clearer examples of the **"one brain, multiple AI tools"** direction.

It is especially useful as a comparison point between:

- general PKM structure,
- AI-agent memory,
- and context portability.

---

## doobidoo/mcp-memory-service

https://github.com/doobidoo/mcp-memory-service

**Focus:** shared persistent memory backend for AI agent pipelines.

### Relevant ideas

- One memory service exposed through MCP, REST, CLI, and other transports.
- Multiple agents sharing one backend.
- Knowledge-graph relationships.
- Self-hosted, vendor-independent memory infrastructure.

### Why it is interesting here

This represents a more service-oriented direction than the file-first approach.

It is useful as a comparison when asking:

> At what point does a human-readable repository stop being enough, and when does a shared memory service become useful?

---

## topoteretes/cognee

https://github.com/topoteretes/cognee

**Focus:** persistent AI memory and knowledge graphs for agents.

### Relevant ideas

- Turning documents, code, and conversations into agent memory.
- Knowledge-graph-oriented retrieval.
- Persistent reuse across sessions.

### Why it is interesting here

Cognee is useful as a reference for the **graph-heavy / retrieval-heavy** end of the design space.

ai-native-brain currently prefers simple human-readable files as the durable layer, so projects like this provide a useful contrast for future scale and retrieval questions.

---

## Comparison dimensions to keep watching

When reviewing related systems, compare them along these axes:

| Dimension | Questions |
| --- | --- |
| Source of truth | Files, database, graph, vector store, hybrid? |
| Human readability | Can a person inspect and edit the memory directly? |
| Retrieval | How is relevant memory selected without loading everything? |
| Provenance | Can a memory be traced back to its source conversation or evidence? |
| Consolidation | Is memory periodically merged, updated, superseded, or forgotten? |
| Temporal history | Can the system answer what it believed at an earlier point in time? |
| Cross-agent use | Can multiple agents / model vendors share the same memory? |
| Human approval | What can the system rewrite or delete without confirmation? |
| Identity / continuity | Does it preserve only facts, or also changing state across sessions? |
| Portability | Can the memory survive switching tools or vendors? |
| Maintenance cost | How much structure must a human maintain manually? |

---

## Current stance

ai-native-brain does not try to select a winner among these approaches.

The working preference is currently:

> keep durable memory human-readable and portable; add retrieval and automation around it only when they earn their complexity.

That may change with experience.

This file exists so those changes can happen deliberately instead of by fashion.
