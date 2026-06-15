---
description: Bootstrap the six Memory Bank files for this project
---

You are initialising the **Memory Bank** for this project (see `CLAUDE.md`).

Goal: populate every file in `memory-bank/` so a future session with **no memory of this
conversation** could resume work using only those files.

Do this:

1. Gather what's already known — read `README.md`, scan `work/` (code/design files),
   skim any notes in `raw/`, and use everything from the current conversation.
2. If critical facts are missing (scope, goals, the problem being solved, key
   components/stack), **ask me** concise questions before writing. Don't invent facts.
3. Fill in each file, replacing the `<!-- guidance -->` placeholders with real content,
   in dependency order:
   - `memory-bank/projectbrief.md` — scope, core requirements, goals (the foundation)
   - `memory-bank/productContext.md` — the problem, stakeholders, success criteria
   - `memory-bank/systemPatterns.md` — architecture, subsystems, key decisions
   - `memory-bank/techContext.md` — technologies/components/suppliers, constraints, deps
   - `memory-bank/activeContext.md` — current focus, next steps
   - `memory-bank/progress.md` — what works, what's left, status
   - `memory-bank/_Index.md` — links + register any known external (non-git) assets
4. Set the `updated:` frontmatter on each file you change to today's date.
5. Keep every file **concise and high-signal** — these are read at the start of every
   task. Summarise; put detail/working in `raw/`.
6. Report a short summary of what you wrote and any gaps still needing my input.

$ARGUMENTS
