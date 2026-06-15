---
type: memory-bank
tier: foundation
updated: 2026-06-15
---

# Project Brief

> **Foundation document — the source of truth.** Everything else in the Memory Bank
> flows from this. It defines scope and goals so they don't drift.

## What this project is

An **MCP (Model Context Protocol) server** that lets an AI assistant (e.g. Claude
Desktop) drive **Microsoft Project** programmatically via **COM automation** on Windows.
It exposes MS Project's project-management capabilities — tasks, dependencies, resources,
calendars, baselines, earned value, critical-path analysis — as **99 MCP tools**. The
entire server is a single Python file, [server.py](../server.py) (~5,200 lines).

## Core requirements

- Expose MS Project operations as MCP tools callable by an LLM, returning JSON.
- Cover the full PM lifecycle: project setup, task CRUD, dependencies, resources,
  scheduling/critical-path analysis, calendars, baselines/earned value, cost/work
  tracking, import/export.
- Be robust against COM quirks: timezone-aware dates, proxy staleness across multiple
  open projects, file locking.
- Each tool self-documents via its docstring (becomes the MCP tool description).

## Goals

1. Let a user manage real MS Project schedules conversationally through an AI assistant.
2. Support PMO rituals (weekly status updates, RAG reporting, variance, what-if delay).
3. Keep the surface broad but consistent — uniform JSON returns, shared helpers.

## Scope

**In scope:**
- Windows + MS Project (tested on 16.0) via COM (`pywin32`).
- Read/query, mutate, analyse, import/export of a `.mpp`/XML project.
- Multi-project awareness (list/switch active project).

**Out of scope:**
- Cross-platform (no macOS/Linux MS Project automation — COM is Windows-only).
- MS Project Server / Project Online / Project for the web (desktop COM only).
- A GUI of its own — interaction is through the MCP client.

## Constraints

- **Windows-only**, requires a running MS Project instance (single COM connection).
- Python 3.10+; depends on `mcp`, `pywin32`, optional `python-dateutil`.
- COM dialogs (e.g. recurring-task insert) are not scriptable → worked around.
- All tests require MS Project running locally.
