---
type: memory-bank
tier: active
updated: 2026-06-15
---

# Active Context

> **Where I left off.** First place to look when resuming. Builds on [[productContext]],
> [[systemPatterns]], [[techContext]].

## Current focus

`hardening` branch merged into `main`. Codebase is at a stable checkpoint with the new
safety layer in place. No active feature in progress.

## Recent changes

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

- [ ] **Push `main`** to origin (local is ahead by the merge + 2 hardening commits) —
      awaiting user go-ahead.
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
