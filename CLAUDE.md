# CLAUDE.md — Memory Bank Protocol

> **I am Claude. My memory resets completely between sessions.**
> The `memory-bank/` folder is my **only** link to everything done on this project
> before now. After every reset I begin entirely fresh — I do not remember the last
> session. I therefore **must** read the Memory Bank at the start of every task, and I
> must maintain it with precision and care. My effectiveness on this project depends
> *entirely* on the accuracy of these files. This is not optional.

---

## 1. At the start of EVERY task — read the Memory Bank first

Before doing anything else, read **all** files in `memory-bank/`. They are kept concise
so this is cheap. Read in dependency order:

1. `memory-bank/projectbrief.md` — what this project is and why (foundation; rarely changes)
2. `memory-bank/productContext.md` — the problem, stakeholders, success criteria
3. `memory-bank/systemPatterns.md` — architecture, subsystems, key decisions
4. `memory-bank/techContext.md` — the stack/components/suppliers, constraints, dependencies
5. `memory-bank/activeContext.md` — **where I left off**: current focus, recent changes, next steps
6. `memory-bank/progress.md` — what works, what's left, known issues

If you are short on time, `activeContext.md` + `progress.md` answer "where was I?" — but
read the whole bank for any non-trivial task. If `memory-bank/` is empty or missing, this
project has not been initialised yet → run `/initialize-memory-bank`.

## 2. How the vault is organised

- **`memory-bank/`** — the **curated**, authoritative, high-signal record. Keep it small
  and true. This is what I read to resume work.
- **`raw/`** — unprocessed capture: session logs (`raw/sessions/YYYY-MM-DD.md`), meeting
  notes (`raw/meetings/`), clippings & dumps (`raw/inbox/`). Append here freely; this is
  never required reading. Raw notes get **distilled** into the memory bank over time.
- **`work/`** — the actual work product (code, design files, calculations). Rename to
  `src/`, `design/`, `cad/`, etc. as suits the project.

The loop: **capture → `raw/` → distill → `memory-bank/`.**

## 3. During work

- Append a dated note to `raw/sessions/YYYY-MM-DD.md` capturing what I did, what I
  learned, and decisions made. This is the source material for later distillation.

## 4. When to update the Memory Bank

Update when **any** of these happen — not just when asked:
- I discover a new pattern, constraint, or fact about the project.
- I make or implement a significant change or decision.
- The user says **"update memory bank"** → review **ALL** files, even ones that may not
  need changes (focus on `activeContext.md` and `progress.md`).

When updating, at minimum keep `activeContext.md` (current focus / recent changes / next
steps) and `progress.md` (status / what's left / known issues) true to reality, and
promote any durable facts from `raw/` into the correct bank file.

## 5. External binaries are NOT in git

CAD files, PDFs, drawings, photos, and spreadsheets are **gitignored** (see `.gitignore`).
Do not commit them. Store them on disk/network/cloud and **reference them by path**.
Register their locations in [`memory-bank/_Index.md`](memory-bank/_Index.md) so they can
be found later.

## 6. Commands

- `/initialize-memory-bank` — bootstrap the six files for a new (or not-yet-documented)
  project. (Natural language: "initialize memory bank".)
- `/update-memory-bank` — review all files and refresh the bank. (Natural language:
  "update memory bank".)

## Memory Bank files
- [projectbrief.md](memory-bank/projectbrief.md)
- [productContext.md](memory-bank/productContext.md)
- [systemPatterns.md](memory-bank/systemPatterns.md)
- [techContext.md](memory-bank/techContext.md)
- [activeContext.md](memory-bank/activeContext.md)
- [progress.md](memory-bank/progress.md)
- [_Index.md](memory-bank/_Index.md)
