---
type: memory-bank
tier: active
updated: 2026-06-16
---

# Active Context

> **Where I left off.** First place to look when resuming. Builds on [[productContext]],
> [[systemPatterns]], [[techContext]].

## Current focus

Tool-discoverability / normalization pass complete in the working tree (uncommitted).
Tool count is now **101** (Phase 8 had raised it to 104; this pass removed 3 thin
wrappers). No other active feature in progress.

## Recent changes

- (2026-06-16) **Discoverability pass** on `server.py` + `README.md` (uncommitted):
  - **P0** server `instructions=SERVER_INSTRUCTIONS` on `FastMCP(...)` with a batching
    rule + single→bulk map (sent to client at init).
  - **P1** every single tool's docstring points to its `bulk_*` counterpart and every
    bulk tool now carries a reverse "prefer this over looping X" line (11 pairs).
  - **P2** `get_tool_guide()` read-only meta-tool already existed (added in Phase 8 —
    the plan's `list_capabilities`, renamed); category map updated for the removals.
  - **P3** `ToolAnnotations(title, readOnly/destructive/idempotentHint)` on **all 101
    tools** (`from mcp.types import ToolAnnotations`). Tally: 40 read-only, 13
    destructive, 26 idempotent-set/update, 22 plain-mutating.
  - **P4** fixed all malformed/missing `Args:` docstrings; removed 2 stale "EXPO 2030"
    refs.
  - **P5** removed thin wrappers `import_xml` / `export_xml` / `search_tasks`
    (breaking) — behaviour folded into `open_project` (.xml), `save_project_as(format=
    "xml")`, `get_tasks(keyword=...)`. README inventory + phase table updated.
  - Verified: `py_compile` passes; an introspection test (count 101, hints, instructions,
    cross-refs) passed. The test + generator scripts were one-offs and deleted.
- (2026-06-15) Merged `origin/hardening` into `main` (merge commit `72b1170`, clean).
  Brought in the **safety hardening layer** (`MSPROJECT_SAFE_ROOT` path allow-list,
  `MSPROJECT_DRY_RUN` switch, short-circuited irreversible deletions, `_launch_app()`
  COM-dispatch unification) and the stderr startup-banner fix. **Not yet pushed.**

- (2026-06-15) Merged `origin/hardening` into `main` (merge commit `72b1170`, clean,
  no conflicts). Brought in the **safety hardening layer** (`MSPROJECT_SAFE_ROOT` path
  allow-list, `MSPROJECT_DRY_RUN` switch, short-circuited irreversible deletions,
  `_launch_app()` COM-dispatch unification) and the stderr startup-banner fix. Verified:
  Memory Bank intact, `server.py` compiles, still 99 tools. **Not yet pushed.**
- (2026-06-15) Initialised the Memory Bank from README + code.
- (2026-06-15) Added Memory Bank scaffold to the repo (commit `b195491`).
- (2026-06-15) **Phase 7** (commit `f5603bb`): critical-path sequence, period filtering,
  what-if delay analysis → 99 tools, 57 new tests (`test_phase7.py`).
- (2026-06-15) **Phase 6** (commit `d631176` + `d7dbd4c`): recurring tasks, resource
  calendars, rate tables, snapshot diff, calendar management, timephased data, variance.

## Next steps

- [ ] **Commit the discoverability pass** (server.py + README.md) — note it includes a
      breaking change (3 wrappers removed). Then **push `main`** (local is ahead by the
      merge + hardening commits + this pass) — awaiting user go-ahead.
- [ ] **Acceptance test (manual, Claude Desktop):** restart, give the original
      "here's a task list, populate the blank project" prompt, confirm a single
      `bulk_add_tasks` call results. This is the real success criterion for the pass.
- [ ] **Run the test suites** on a Windows machine with MS Project to validate the merge;
      the hardening layer reworked file paths and COM dispatch. Remember to set
      `MSPROJECT_SAFE_ROOT` (scratch dir) and `MSPROJECT_DRY_RUN=0` first.
- [ ] If touching code: follow the `@mcp.tool()` + `get_app()`/`get_proj()` + JSON-return
      pattern, route file paths through `_resolve_safe_path()`, persist via `_save()`, add
      a test to the matching phase suite.

## Active decisions & considerations

- Single-file `server.py` is intentional (~5,200 lines) — no plan to split into a package
  yet; revisit only if it becomes unmanageable.
- Recurring tasks remain simulated (COM dialog limitation) — known acceptable trade-off.
- **Fail-closed file access**: unset `MSPROJECT_SAFE_ROOT` blocks all file tools by
  design. Watch for confusion if a fresh deployment/test run forgets to set it.
- Indirect prompt injection from untrusted `.mpp`/`.xml` is an accepted, documented
  residual risk (path-confinement + dry-run mitigate but don't eliminate it).
