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
3. Set environment variables (read once at startup):
   - **`MSPROJECT_SAFE_ROOT`** — directory every file-taking tool is confined to.
     **Required**: if unset, all file operations are refused. Set to the folder holding
     your project files (e.g. `C:\Projects`).
   - **`MSPROJECT_DRY_RUN`** — optional; `1`/`true`/`yes`/`on` makes mutating tools skip
     saves and irreversible deletions return a preview. Default off.
4. Register in `claude_desktop_config.json` under `mcpServers.msproject` →
   `python /path/to/server.py` (pass the env vars in the `env` block), OR run standalone
   `python server.py`.
5. Tests: `python tests/test_phaseN.py` — all require MS Project running, **and now
   require `MSPROJECT_SAFE_ROOT`** pointing at a writable scratch dir with
   `MSPROJECT_DRY_RUN=0` (they open and save real files).

## Constraints & dependencies

- **`MSPROJECT_SAFE_ROOT` must be set** or every file-taking tool refuses to run
  (fail-closed). See [[systemPatterns]] for the safety layer.
- **Windows + COM only** — no cross-platform support.
- Single COM connection — don't open MS Project GUI dialogs while the server is active
  (file locking); proxies go stale across projects → `switch_project` first.
- `undo_last` supports up to 10 consecutive undos (COM undo less reliable than UI).
- `get_timephased_data` slow on large ranges — keep to weeks/months.
- Gitignored: `__pycache__/`, `*.pyc`, `*.pyo`, `.env` (see [.gitignore](../.gitignore)).
