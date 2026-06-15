---
type: memory-bank
tier: context
updated: 2026-06-15
---

# Product Context

> **Why this project exists.** Builds on [[projectbrief]].

## The problem

MS Project is powerful but interaction is manual and GUI-bound. Project managers spend
time on repetitive, error-prone rituals: updating progress, recalculating schedules,
chasing the critical path, producing RAG/variance reports, running what-if scenarios.
There is no good way to drive these from an AI assistant — MS Project has no modern API,
only Windows COM automation, which is awkward to use directly. Without this server, an
LLM cannot read or change a real project plan.

## Who it's for / stakeholders

- **Project / programme managers** running real MS Project schedules who want to work
  conversationally via an AI assistant (Claude Desktop).
- **PMO analysts** doing weekly status updates, RAG reporting, and variance analysis.
- **Developers** integrating MS Project into AI/automation workflows via MCP.

## How it should work (intended experience)

The user has MS Project open with a plan loaded. They talk to their AI assistant in
natural language ("mark everything complete through last Friday", "what happens if Task
12 slips a week", "show me the critical path for Q2", "which resources are overallocated").
The assistant calls the relevant MCP tool(s); the server executes the COM operations and
returns structured JSON the assistant turns into an answer or a confirmed change.

## Success criteria

- An LLM can perform the full PM lifecycle against a live project without the user
  touching the MS Project GUI.
- Tools return consistent, parseable JSON and degrade gracefully on COM errors.
- Common PMO rituals (status update, RAG, critical path, variance, what-if) are each a
  single tool call.
- Test suites pass against a live MS Project instance (currently 202 tests, 7 suites).
