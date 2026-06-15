---
type: memory-bank
tier: active
updated: 2026-06-15
---

# Active Context

> **Where I left off.** First place to look when resuming. Builds on [[productContext]],
> [[systemPatterns]], [[techContext]].

## Current focus

Phase 7 is complete (99 tools). Memory Bank just initialised. No active feature in
progress — the codebase is at a stable, fully-tested checkpoint.

## Recent changes

- (2026-06-15) Initialised the Memory Bank from README + code.
- (2026-06-15) Added Memory Bank scaffold to the repo (commit `b195491`).
- (2026-06-15) **Phase 7** (commit `f5603bb`): critical-path sequence, period filtering,
  what-if delay analysis → 99 tools, 57 new tests (`test_phase7.py`).
- (2026-06-15) **Phase 6** (commit `d631176` + `d7dbd4c`): recurring tasks, resource
  calendars, rate tables, snapshot diff, calendar management, timephased data, variance.

## Next steps

- [ ] No committed next feature. Candidate directions if work resumes: more reporting
      tools, performance work on `get_timephased_data`, or hardening COM error handling.
- [ ] If touching code: follow the `@mcp.tool()` + `get_app()`/`get_proj()` + JSON-return
      pattern, add a test to the matching phase suite, run all suites against live MS Project.

## Active decisions & considerations

- Single-file `server.py` is intentional (~5,200 lines) — no plan to split into a package
  yet; revisit only if it becomes unmanageable.
- Recurring tasks remain simulated (COM dialog limitation) — known acceptable trade-off.
