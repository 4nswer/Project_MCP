---
type: memory-bank
tier: context
updated: 2026-06-15
---

# System Patterns

> **How it's built / organised.** Builds on [[projectbrief]].

## Architecture overview

Single-file MCP server using the **FastMCP** framework (`mcp = FastMCP("MS Project")` in
[server.py](../server.py)). Each tool is a `@mcp.tool()`-decorated function. Tools obtain
the live MS Project COM application via `get_app()` and the active project via
`get_proj(app)`, perform COM operations, and return a JSON string. `mcp.run()` starts the
stdio server.

```
AI client (Claude Desktop)  ──MCP/stdio──▶  server.py (FastMCP, 99 tools)
                                                  │ pywin32 COM
                                                  ▼
                                          MS Project (Windows, running instance)
```

## Subsystems / components & relationships

Tools are grouped (see [README](../README.md) for the full inventory) into: Project
Management, Task Queries, Task Mutations, Dependencies, Resources & Assignments, Rate
Tables, Custom Fields, Import/Export, Calendars & Working Hours, Scheduling & Analysis,
Status Date & Progress, Timephased Data, Baselines & Earned Value, Variance/Reporting,
Cost & Work, Progress Tracking, Advanced Operations, Multi-Project, Filtering/Grouping,
Connectivity. All share the same COM-access and date helpers.

## Key technical decisions

- **Single-file server** (~5,200 lines) — keeps the project simple to deploy/register; no
  package structure. New tools appended in place.
- **COM via pywin32** (2024-era choice) — the only programmatic interface to desktop MS
  Project; no REST/API alternative exists for the desktop product.
- **JSON-string returns from every tool** — uniform, LLM-friendly, parseable.
- **`_to_naive()` date normalization** — COM may return timezone-aware datetimes;
  normalizing avoids naive/aware comparison errors against `datetime.now()`.
- **`switch_project` before cross-project ops** — COM proxies go stale when multiple
  projects are open; explicit switching is required.
- **Recurring tasks simulated** — `RecurringTaskInsert` is a dialog-only COM method, so
  `add_recurring_task` creates individual occurrences under a summary task (needs
  `python-dateutil`).
- **Phased development** — features added in numbered phases 1–7 (see [[progress]]),
  each with its own test suite.

## Conventions & patterns in use

- COM access: always `app = get_app()` then `proj = get_proj(app)`.
- Dates: `_parse_date()` for `YYYY-MM-DD` input → COM; `_fmt_date()` for output;
  `_to_naive()` before comparing COM dates.
- Every tool returns `json.dumps({...}, indent=2)`; docstrings ARE the tool descriptions.
- Tasks referenced by **UniqueID**. Custom fields (Text1–30, Number1–20, etc.) used for
  things like RAG status (RAG lives in **Text1**).
- Tests organised by phase under [tests/](../tests/); each creates a temporary project,
  asserts, and cleans up. **MS Project must be running** to test.
