---
description: Review ALL Memory Bank files and refresh them to match reality
---

You are performing a full **Memory Bank** update (see `CLAUDE.md`).

Per the protocol, when asked to "update memory bank" you **review every file**, even ones
that may not need changes — but focus effort where reality has moved on.

Do this:

1. Read **all** files in `memory-bank/` and the recent notes in `raw/sessions/`.
2. Reconcile each file against what has actually happened (this conversation, changes in
   `work/`, decisions made):
   - `activeContext.md` — **update first and most carefully**: current focus, recent
     changes (newest first, dated), next steps.
   - `progress.md` — move finished items to "what works", update status, log new known
     issues.
   - `systemPatterns.md` / `techContext.md` — add any new decisions, components, or
     constraints discovered.
   - `projectbrief.md` / `productContext.md` — change only if scope or goals genuinely
     shifted (these are meant to be stable).
   - `_Index.md` — register any new external (non-git) assets and useful raw notes.
3. **Distill**: promote durable facts from `raw/` into the right bank file; keep the bank
   concise — trim anything stale or superseded.
4. Set the `updated:` frontmatter to today's date on each file you change.
5. Report a short summary of what changed and why.

$ARGUMENTS
