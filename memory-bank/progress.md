---
type: memory-bank
tier: active
updated: 2026-06-16
---

# Progress

> **Status of the whole project.** Complements [[activeContext]] (near-term view).

## What works / is done

- **Safety hardening layer** (merged into `main` 2026-06-15): `MSPROJECT_SAFE_ROOT` path
  allow-list, `MSPROJECT_DRY_RUN` switch, short-circuited irreversible deletions,
  stderr startup banner. `server.py` compiles; merge clean. See [[systemPatterns]].
- **101 MCP tools** spanning the full PM lifecycle (see [README](../README.md) inventory).
  Phase 8 added bulk-completeness tools + `get_tool_guide` (→104); the 2026-06-16
  discoverability pass removed 3 thin wrappers (→101).
- **Discoverability/normalization pass** (2026-06-16, uncommitted): server `instructions`,
  `ToolAnnotations` on every tool, single↔bulk cross-references, docstring normalization,
  removal of `import_xml`/`export_xml`/`search_tasks`. `py_compile` + introspection pass.
- Enriched task data (35+ fields) returned by all task queries.
- **202 tests across 7 suites**, all passing against a live MS Project:
  `test_new_tools.py` (11), `test_phase2.py` (10), `test_phase3.py` (15),
  `test_phase4.py` (23), `test_phase5.py` (11), `test_phase6.py` (75), `test_phase7.py` (57).
- Phases 1–7 complete: core CRUD → resources/baselines → custom fields/calendars/
  scheduling → advanced ops/multi-project/filtering → cost/work → timephased/variance/
  calendar mgmt → critical-path intelligence & what-if.

## What's left to build

- [ ] No committed roadmap beyond Phase 7. Open candidates: richer reporting,
      timephased-data performance, COM error-handling hardening.

## Current status

**Stable checkpoint with hardening merged + discoverability pass staged.** All phases +
safety layer on `main`; the 2026-06-16 discoverability pass is in the working tree
(uncommitted). **Local `main` not yet pushed**; merge + pass not yet re-tested on Windows.

## Known issues & open problems

- **Hardening not re-tested on a live MS Project** since the merge — test suites need a
  Windows machine and now require `MSPROJECT_SAFE_ROOT` set.
- **Fail-closed file access**: file tools refuse to run if `MSPROJECT_SAFE_ROOT` is unset
  (by design — but a deployment/test gotcha).
- **Indirect prompt injection** from untrusted `.mpp`/`.xml` files is a documented
  residual risk the safety layer does *not* fully eliminate.

- **COM proxy staleness** across multiple open projects → must `switch_project` first.
- **Undo** limited to 10 consecutive undos; COM undo less reliable than the GUI.
- **File locking** — only one COM connection; avoid MS Project GUI dialogs while running.
- **Timezone-aware dates** from COM — normalized via `_to_naive()`.
- **Recurring tasks** simulated (occurrences under a summary task); needs `python-dateutil`.
- **`get_timephased_data`** slow on large ranges — restrict to weeks/months.
- All testing requires a Windows machine with MS Project running (no CI possible without it).
