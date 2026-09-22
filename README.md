# ai-native-brain

> A living experiment in shared external memory for humans and AI.

**ai-native-brain** is an experiment in building a personal knowledge and memory system that is useful to both a human and the AI agents they work with.

It started from a practical problem:

- important context gets trapped inside individual chats,
- a new session often starts without the reasoning that led to past decisions,
- different AI tools do not naturally share the same long-term context,
- and ordinary notes are usually written for humans first, with AI added later.

This repository explores the opposite direction:

> **What does a "second brain" look like when humans and AI are both first-class readers and writers?**

The system is intentionally simple today: plain Markdown, Git history, explicit structure, and selective retrieval. It is not presented as a finished framework. The structure is expected to change as it is used.

## What this repository contains

This public repository contains the **shareable architecture, operating ideas, and templates**.

It does **not** contain the private working memory, personal conversations, project details, or identity-specific long-term memories from the system that inspired it.

The private system and the public pattern are deliberately separated.


## Who this is for

This repository is **not intended as a "build your own brain in 10 minutes" starter kit**.

It is primarily for people who are already experimenting with things like:

- persistent AI memory,
- agent memory across sessions,
- AI-native PKM / second-brain systems,
- multi-agent context sharing,
- human-readable long-term memory,
- continuity across chats, tools, or model vendors.

The goal is to make the design choices, trade-offs, failures, and evolving structure visible enough to be useful as a **reference implementation / research notebook**.

The templates are examples of the current structure, not a recommended universal schema.


## Core idea

The "brain" is not one giant prompt.

It is a set of small, durable artifacts with different jobs:

```text
conversation / work
        ↓
   observations
        ↓
      Seeds
        ↓
 repeated evidence
        ↓
 Principles / Decisions
        ↓
 projects and future conversations
```

AI reads only the parts needed for the current task instead of loading the entire history every time.

## Main layers

### 1. Principles

Stable decision criteria that should survive individual projects.

Examples:

- how to balance speed and quality,
- when to preserve an idea instead of implementing it,
- how humans and AI divide roles.

### 2. Decisions

Important choices together with their reasoning.

A useful decision record answers:

1. What was decided?
2. Why?
3. What alternatives were not chosen?
4. Where does this decision apply?

The goal is not only to remember the result, but to make the reasoning reconstructable later.

### 3. Seeds

Unfinished ideas that are worth keeping but are not yet "truth".

A Seed can remain dormant, grow through repeated observations, or eventually become a Principle or Decision.

```text
seed → growing → principle / decision
          ↘
          dormant
```

This avoids forcing every interesting thought into an active project.

### 4. Projects

Stable entry points for active areas of work.

Project pages should help a human or AI quickly answer:

- What is this?
- Why does it exist?
- What belongs here?
- Where is the current source of truth?

Fast-changing implementation details can live elsewhere.

### 5. Operating System

Rules for how the whole system is used:

- what gets written,
- where it goes,
- when to review it,
- how multiple AI agents share context,
- and how to avoid turning knowledge management into its own full-time project.

## Continuity memory

A second line of experimentation focuses on **continuity across sessions and models**.

Instead of treating memory as one flat database, the system separates several human-readable concepts:

- **Episode / Bookmark** — a moment worth carrying forward.
- **Current state / Breath** — what still feels active and relevant now.
- **Handoff** — enough context for a future session to continue naturally.
- **Dream / Consolidation** — periodically looking back, reconnecting recent experience with older memory, and deciding what should remain important.

These names are interface metaphors, not claims that an AI has a human brain.

The useful part of the metaphor is operational: humans already understand ideas such as remembering, forgetting, sleeping on something, and carrying context into a new day.

See [docs/continuity-memory.md](docs/continuity-memory.md).

## Design principles

- **Files are the source of truth.** Indexes and retrieval layers should be replaceable.
- **Human-readable first.** A person should be able to inspect and edit the memory directly.
- **AI-readable by design.** Names, metadata, and navigation should help models retrieve only what matters.
- **Preserve reasoning, not just conclusions.**
- **Do not promote every idea to truth.** Keep uncertainty explicit.
- **Do not load everything.** Prefer navigation and selective retrieval over giant context dumps.
- **History matters.** Updates should preserve how understanding changed over time.
- **Private memory and public patterns are different products.**
- **The memory system itself is allowed to evolve.**

## Repository structure

```text
ai-native-brain/
├── README.md
├── docs/
│   ├── architecture.md
│   ├── continuity-memory.md
│   └── landscape.md
└── templates/
    ├── seed.md
    ├── decision.md
    ├── principle.md
    └── project.md
```

This repository begins with observations and design patterns rather than a large implementation. The structure is meant to be inspected, compared, and questioned rather than copied wholesale.

## Why Git + Markdown?

Because the system should remain:

- portable,
- inspectable,
- diffable,
- versioned,
- searchable,
- usable without a specific model vendor,
- and easy for both humans and agents to navigate.

A future version may add full-text search, vector retrieval, knowledge graphs, automatic consolidation, or agent tooling. Those should enhance the files, not make the files disposable.

## Related fields

This experiment overlaps with several existing areas:

- Personal Knowledge Management (PKM)
- Second Brain systems
- AI-native PKM
- Agent memory
- Long-term / persistent AI memory
- Context management
- Memory consolidation
- Personal AI infrastructure
- External cognition

There is no claim that the terminology or mechanisms here are novel in isolation. The goal is to document a practical combination that has been useful in real human-AI work, compare it with adjacent systems, and leave useful notes for others exploring the same problem space.

See [docs/landscape.md](docs/landscape.md) for related projects and comparison notes.

## Status

**Experimental / living system.**

The current structure is not considered final.

A major goal of this repository is to keep watching the wider agent-memory and AI-native knowledge-management space, test useful ideas in practice, and evolve the architecture without losing the simplicity of human-readable files.

## Public / private boundary

This repository intentionally publishes **the method, not the memory**.

Good candidates for public material:

- architecture,
- generic templates,
- operating rules,
- anonymized examples,
- lessons learned.

Keep private:

- personal conversations,
- private project strategy,
- employer or client information,
- personal profiles,
- credentials,
- identity-specific long-term memory.

That boundary is part of the design, not an afterthought.
