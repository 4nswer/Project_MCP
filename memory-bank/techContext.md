---
type: memory-bank
tier: context
updated: 2026-06-15
---

# Tech Context

> **The "stack".** Builds on [[projectbrief]].

## Technologies / tools

- **Python 3.10+** — single-file server, [server.py](../server.py).
- **MCP / FastMCP** (`mcp` package, `mcp.server.fastmcp.FastMCP`) — MCP server framework;
  runs over stdio via `mcp.run()`.
- **pywin32** — COM automation bridge to MS Project on Windows.
- **python-dateutil** (optional) — only needed for `add_recurring_task` recurrence math.
- **Microsoft Project** desktop, Windows (tested on **16.0**) — must be running.

## Key components / materials

| Item | Spec / version | Source | Notes |
|------|----------------|--------|-------|
| MS Project | desktop 16.0 | Microsoft | Windows-only; COM target; must be running |
| Python | 3.10+ | python.org | |
| mcp | latest | `pip install mcp` | FastMCP framework |
| pywin32 | latest | `pip install pywin32` | COM access |
| python-dateutil | optional | `pip install python-dateutil` | recurring tasks only |

## Suppliers & references

- README: [README.md](../README.md) — full 99-tool inventory + known limitations.
- Contributing/conventions: [CONTRIBUTING.md](../CONTRIBUTING.md).
- No external binary assets currently tracked (see [[_Index]]).

## Setup / environment

1. Windows with MS Project installed and **running** (open a file, or the server can
   create one).
2. `pip install mcp pywin32` (+ `python-dateutil` for recurring tasks).
3. Register in `claude_desktop_config.json` under `mcpServers.msproject` →
   `python /path/to/server.py`, OR run standalone `python server.py`.
4. Tests: `python tests/test_phaseN.py` — all require MS Project running.

## Constraints & dependencies

- **Windows + COM only** — no cross-platform support.
- Single COM connection — don't open MS Project GUI dialogs while the server is active
  (file locking); proxies go stale across projects → `switch_project` first.
- `undo_last` supports up to 10 consecutive undos (COM undo less reliable than UI).
- `get_timephased_data` slow on large ranges — keep to weeks/months.
- Gitignored: `__pycache__/`, `*.pyc`, `*.pyo`, `.env` (see [.gitignore](../.gitignore)).
