# Help or Yelp

**A community-driven platform connecting people who need help with those willing to offer it** — the longest-running project in this portfolio: **162 commits from July 2025 to June 2026, ~39K lines of code, 163 automated tests**.

> Private repository — code walkthrough available on request.

## What it does

Users post requests for help (or offers of help) with location and expiry; others respond, coordinate, and rate the experience. Think of it as a neighborhood mutual-aid board with real accounts, moderation, and messaging.

## Architecture

| Layer | Technology |
|---|---|
| Backend | .NET 9, ASP.NET Core — layered (Domain / Application / Infrastructure / Controllers) |
| Frontend | React, TypeScript |
| Messaging | RabbitMQ |
| Database | PostgreSQL, hand-written SQL migrations |
| Infra | Docker Compose |

The repo includes organized documentation: product summary and backlog, a backend architecture document with an HTML diagram, and setup/infrastructure guides.

## Why it's interesting engineering-wise

- This is the project where my workflow *changed*: it started in mid-2025 as conventional solo development and crossed into agentic development in early 2026 — its commit history is the before/after picture in one repo
- Event-driven pieces run through RabbitMQ rather than everything being a synchronous HTTP call
- Post lifecycle (creation, location attachment, expiration) is handled with explicit SQL migrations — no magic

[← Back to portfolio](../README.md)
