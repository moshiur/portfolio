# Personal Co-Worker

**A self-hosted, model-agnostic personal AI co-worker built in .NET** — the newest project in the portfolio (started June 2026) and the most direct expression of how I think AI systems should be built.

> Private repository — code walkthrough available on request.

## What it is

An orchestration layer with memory and tools wrapped around an *interchangeable* model — not a custom-trained model. The model is the swappable part; the value is the system around it:

- A durable agent loop
- A **four-tier memory subsystem** — `semantic` / `episodic` / `working_state` / `profile` — in a single PostgreSQL + pgvector store
- A real side-effect / confirmation boundary (nothing non-read-only happens without a gate)
- Observability from day one — OpenTelemetry traces, logs, and cost tracking into the .NET Aspire dashboard

The first slice is a daily market brief: a scheduled agent gathers market data, pulls context and yesterday's brief from memory, produces the brief in a fixed format, and writes a summary back to memory.

## Architecture

| Layer | Technology |
|---|---|
| Runtime | .NET, Microsoft Agent Framework (the Semantic Kernel + AutoGen successor) |
| Memory | PostgreSQL + pgvector, idempotent embedded SQL migrator |
| Model access | `Microsoft.Extensions.AI` `IChatClient` — swappable provider, optional local model via Ollama |
| Observability | OpenTelemetry → .NET Aspire dashboard |

## The one rule

> **Build the slice, not the platform.** Scope is the only thing that kills a project like this.

Phase 1 (memory schema, migrator, pgvector verification) is complete; Phase 2 (retrieval) is in progress — the repo carries an explicit `ROADMAP.md`, `ARCHITECTURE.md`, and a `CLAUDE.md` working contract that the coding agent follows.

## Why it's interesting engineering-wise

- Working *with* AI agents daily teaches you what they lack: durable memory, confirmation boundaries, and observability — this project builds exactly those
- Four memory types in one store forces honest schema design instead of "throw it all in a vector DB"
- Cost observability is a first-class feature: every model call is traced and priced

[← Back to portfolio](../README.md)
