# Sizing and capacity

## Why points and not tokens

Nobody, including you, knows the exact token budget of a plan. Providers change limits, budgets depend on the model chosen, and they aren't published precisely. So vibe-plus uses **relative** sizes and learns each user's real capacity from their log. A wrong first guess is fine as long as it's corrected after a window or two.

## What makes a task expensive

Cost rises with how much the agent has to **read**, **re-read**, and **retry**:

- Large or many files in context, and whole-repo exploration
- Long conversations (the full history is re-sent every turn)
- Debug loops: run, fail, read the log, edit, run again
- Many tool calls in agent mode (each one adds output to the context)
- Images and screenshots
- Bigger or "thinking" models (the same task can cost several times more)

What keeps a task cheap: a precise goal, a short list of files, and a clear done-check, so the agent knows when to stop.

## Sizes

| Size | Points | Typical shape | Examples |
|------|--------|---------------|----------|
| **S** | 1 | One file, clear spec, little reasoning | Add a field to a form; write tests for one existing function; fix copy or styles; add an env var and config; small README section |
| **M** | 2 | 2–4 files, one feature, some wiring | New page or component wired to an existing API; a CRUD endpoint plus a test; a simple DB migration plus a model; set up linting and formatting |
| **L** | 4 | New subsystem, external integration, or real uncertainty | Initial project scaffold; auth (sign up, log in, session); payments or webhook integration; a hard bug with unknown cause; a deploy pipeline the first time |

**Bigger than L: split it.** Split along seams that each leave the app working:

- By layer: data model, then API, then UI.
- By path: the happy path first, then errors and edge cases.
- Spike, then build: an S/M "spike" to learn how the library or API behaves (write the notes into the handoff), then the real task.

**Size up one step** when the user is new to coding (more back-and-forth), when the area of code is unfamiliar or messy, or when the task involves a library the model may not know well.

## Default starting capacity (points per window)

These are only starting guesses, and the log overrides them after the first window or two.

| Situation | Start at |
|-----------|----------|
| Claude Pro, mid-tier model (Sonnet-class), Claude Code | 8 |
| Claude Pro, top-tier model (Opus-class) | 4 |
| ChatGPT Plus, Codex (CLI, IDE or cloud) | 8 |
| Chat-only in a browser (copy-paste coding) | 6 |
| Gemini, Cursor, Copilot or other paid tiers | 8 |
| Unknown | 6 |

**Plan to capacity − 1** (keep one point as buffer) **plus the wrap-up**, which is reserved and not counted.

A typical 8-point window looks like `L + M + S + S` or `M + M + M + S`. Don't build windows out of eight S tasks: each task has a fixed start-up cost (kickoff and reading files), so very small tasks waste budget. Merge adjacent S tasks that touch the same files.

## Recalibration rule (run at every check-in)

Keep a log row per window: `planned`, `done`, `limit_hit` (y/n).

1. **Limit hit before the plan was done**: that window's real capacity = `done`.
2. **Plan finished and the limit was never hit**: that window's real capacity = `done + 2` (they had room left, so probe upward).
3. **Plan finished right as the limit hit**: real capacity = `done`. The estimate was right.
4. **New capacity** = the average of the last 3 windows' real capacity, rounded down. With fewer than 3 windows, average what you have.
5. If a single task blew far past its size (an M that took the whole window), don't change capacity. **Re-size that kind of task** in the rest of the plan instead. The estimate was off, not the window.

After recalibrating, re-pack the remaining windows and tell the user in one line, for example: "Capacity is now 6 points per window, so the plan moves from 9 windows to 11."

## Weekly caps

If the plan has a weekly cap, ask the user (or note in Assumptions) how many full windows they get per week before hitting it. Plan no more than that per week. If the weekly cap is the bottleneck, push more work into 🧑 tasks and `small-ok` model tasks.
