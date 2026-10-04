---
name: vibe-plus
description: Plans a software project and splits it into right-sized tasks packed into usage windows, so people on entry-level AI plans (Claude Pro, ChatGPT Plus / Codex, Gemini, Cursor or Copilot paid tiers, and similar) get the most out of each ~5-hour usage reset. Use this whenever someone mentions hitting usage or rate limits ("you've reached your limit", "out of messages", "limit resets at 3pm"), says they're on Pro/Plus rather than Max/Pro-200, wants to build something across several sessions or days with an AI coding agent, or asks to break a project into tasks, sprints, milestones or a roadmap for vibe coding, even if they never say "vibe-plus". Also use it at the start of a session when a `vibe-plus/` folder or `HANDOFF.md` exists, to resume the plan, and when a window just ended, to log progress and re-plan.
---

# vibe-plus

People on entry-level plans don't usually run out of ideas. They run out of usage, often in the middle of a task, which leaves the code half-changed and the agent's context gone. Then the next session spends a big part of the new window working out where things stood. vibe-plus prevents that by planning the work around the usage window:

- **Right-sized tasks.** Every task can finish well inside one window and ends in a working, committed state.
- **Packed windows.** Each window gets about as much work as it can hold, with the riskiest task first and room left for wrap-up.
- **Cheap restarts.** A short handoff file lets a fresh session pick up where the last one stopped without exploring the repo again.
- **Useful cooldowns.** Jobs that don't need an AI (accounts, API keys, assets, manual testing) are planned for the hours while the limit resets.

## Vocabulary

- **Window**: one usage period, from first message until the limit resets (about 5 hours on most plans). Many plans also have a **weekly cap**, so the plan respects that too.
- **Points**: relative task cost. **S = 1, M = 2, L = 4.** Nothing is bigger than L, so anything bigger gets split.
- **Capacity**: how many points fit in one window for this user, with their tool and model. It starts as a guess and is corrected using the log (see `references/sizing.md`).
- **🤖 task**: done with the AI. **🧑 task**: done by the human, ideally during a cooldown.

## Pick the mode

Check the situation first, since the right action depends on it:

1. **A `vibe-plus/` folder exists, or the user pastes a handoff block**: go to **Resume**.
2. **The user says the limit hit, the window ended, or "log my progress"**: go to **Check-in**.
3. **Otherwise**: go to **New plan**.

## Mode: New plan

### 1. Intake (one message, not many)

Every turn uses budget, so ask everything you need in **one** batched message and skip anything the user already said. Ask for:

- What they're building, and who it's for (one or two sentences is enough).
- Which tool and plan they use (for example Claude Pro in Claude Code, ChatGPT Plus with Codex, or claude.ai in the browser). This decides capacity and whether files can be written.
- Whether there's existing code, or this is a fresh start.
- How many windows they can realistically use: per day, which days, and any deadline.
- Their comfort level with code. This changes how much a 🧑 task can ask of them.

If the user clearly wants you to just go ahead, make reasonable assumptions, list them in the plan under "Assumptions", and continue.

If there is existing code, look only at what you need: the README, the manifest file (`package.json`, `pyproject.toml`, ...), and the top-level layout. A full-repo exploration can cost a big share of a window, and the plan doesn't need it.

### 2. Lock decisions up front

Write down the choices that would otherwise get reopened in every session: the stack, the main libraries, folder structure, hosting, and data storage. Reopening a decision costs a window and often triggers a rewrite. Suggest **boring, popular** tools: models know them well, so there are fewer correction loops. Cut scope to a real MVP and park everything else under "Later". A smaller finished project beats a bigger half-done one.

### 3. Break the work down

Milestones first, each a demo-able step such as "can sign up" or "can post an item". Then split each milestone into tasks. A full task card has:

- **Size** (S/M/L) and **🤖/🧑**.
- **Goal**: one sentence.
- **Files**: what it creates or touches. This keeps the agent from wandering.
- **Context**: the only files or docs the agent must read for it.
- **Done when**: a check anyone can run, for example "`npm test` passes", "page at /login renders and submits", or "curl returns 201".
- **Kickoff prompt**: a ready-to-paste prompt that starts a fresh conversation on this task. It names the goal, the files, the done-check, and says "commit when done".
- Optionally **Model**: `small-ok` when a cheaper or faster model can handle it (boilerplate, tests, docs, copy), `big` for architecture or hard debugging. Use this only if the user's tool lets them pick a model.

For anything larger than L, split it. A task that dies halfway at the limit is the most expensive kind: you pay for it twice, and the repo is broken in between. `references/sizing.md` has the sizing guide and examples.

**Just-in-time detail.** Write full cards only for the **next window or two**. Every other task gets a **one-liner**: `ID · size · 🤖/🧑 · title · done when <check>`. There are two reasons:

- The plan is written using the user's own allowance. A 350-line plan file can cost a real share of the first window before any code exists.
- Cards for windows far ahead go stale. Recalibration re-packs them, earlier tasks change file names, and gotchas show up. A card written just before its window uses what was actually learned.

Later windows still need to be planned properly. The one-liner keeps the size, the order and the done-check, so packing and recalibration still work, and the locked decisions keep later tasks on track. Expand a window's one-liners into full cards at the **Resume** or **Check-in** right before that window (see those modes).

### 4. Pack the windows

Fill windows up to about **capacity minus a buffer**. Default capacity is in `references/sizing.md`; adjust it for the user's tool. In each window:

1. **Start**: read the handoff. This is nearly free and isn't a task.
2. **The riskiest or biggest task first**, so that if it goes sideways there's budget left in the same window to recover.
3. Then medium and small tasks, in dependency order.
4. **Wrap-up (always reserved)**: update `HANDOFF.md`, tick boxes, commit. Running out before this step is how state gets lost, so never plan it away.

Put 🧑 tasks in the **cooldown** between windows, and make sure no 🤖 task is blocked on a 🧑 task scheduled after it. Keep the weekly cap in mind if they gave you one: don't plan more windows per week than they can use.

### 5. Write it down

**Agent with file access** (Claude Code, Codex CLI, Cursor, ...): create

- `vibe-plus/PLAN.md` from `assets/plan-template.md`, with full cards for **W1 and W2** and one-liners after that. Aim for under about 200 lines. Two windows of cards means a user doing back-to-back windows (a Saturday, say) can start W2 without a planning step.
- `vibe-plus/HANDOFF.md` from `assets/handoff-template.md`

Then **offer** (don't just do it) to add one line to the project's agent instructions file (`CLAUDE.md`, `AGENTS.md`, `.cursorrules`, or `GEMINI.md`): `At the start of each session, read vibe-plus/HANDOFF.md first and do not explore the repo beyond what the current task lists.` Agents load that file automatically, so every new session starts cheaply.

**Chat-only** (claude.ai or chatgpt.com in a browser, no file access): use the **compact plan** in `assets/chat-plan-template.md`. Here every line you write is generated inside the user's own chat, so it comes out of the same limit the plan is meant to protect. A 300-line plan can burn a noticeable part of the first window before any code exists. The compact plan works like this:

- **Plan in one block, about 60–80 lines.** The decisions, MVP and Later lists, assumptions, the window table, and **one line per task**: `ID · size · title · done-when`. No goal, files or context fields for later tasks. The one-liner plus the locked decisions is enough until that window arrives.
- **Full cards only for W1:** the task cards with their kickoff prompts. Later windows get their cards just in time, at each check-in or resume. That costs the same in total, but it's spread across windows, and cards written later reflect what was actually learned, so they don't go stale after a recalibration.
- **A short starter handoff block** (about 10 lines) to paste at the start of the next chat.
- **Shared rules said once, not in every prompt.** Put repeated instructions ("return full files", "two failed fixes, stop") in the Project instructions, and keep the kickoff prompts to what's specific to the task.

Aim for the **whole reply to stay under about 150 lines**. Suggest storing the plan and the latest handoff in a Project (Claude Projects, ChatGPT Projects) so they persist, and tell the user that each check-in will hand over the next window's prompts.

### 6. Close the planning turn

Planning uses budget too, so keep the reply short. Include:

- The window-by-window overview (a compact table).
- What to do **right now** (the first kickoff prompt).
- What to do in the first cooldown (🧑 tasks).
- A one-line reminder: start a **fresh conversation per task** and paste the kickoff prompt.

## Mode: Resume

1. Read `vibe-plus/HANDOFF.md` (or the pasted block). Read `PLAN.md` only for the current window's task cards. Don't re-explore the repo: the handoff exists so the session doesn't have to.
2. Say in two or three lines where things stand and what this window holds.
3. If `HANDOFF.md` lists gotchas or a broken state, deal with that first.
4. If this window's tasks are still one-liners, expand them into full cards with kickoff prompts now, for **this window only**. With file access, write them into `PLAN.md`; in chat-only, put them in the reply. Use what the handoff says (real file names, gotchas), which is why this waits until now.
5. Start the first task, or hand over its kickoff prompt if the user prefers one conversation per task.

## Mode: Check-in

Run this at the end of a window, or when the limit hits:

1. Ask (or infer from git log and checkboxes) which tasks finished and whether the limit hit early, on time, or never. If a task was left half-done, follow **Unfinished tasks** below as part of this check-in.
2. Append a line to the **Log** in `PLAN.md`: date, window, points planned, points done, limit hit (y/n), and a note.
3. **Recalibrate capacity** with the rule in `references/sizing.md`. Re-pack the remaining windows if capacity changed or a task turned out bigger than planned (split it now).
4. Rewrite `HANDOFF.md`: the next task, the current state, gotchas, and any uncommitted or broken bits.
5. Remind them which 🧑 tasks fit this cooldown and when the next window starts, if they told you their reset time.
6. **Keep the lookahead.** With file access, make sure the next window has full cards in `PLAN.md`, and expand it now if it doesn't. Leave windows beyond that as one-liners.
7. **Chat-only:** give back the updated handoff block plus the **next window's** full cards and kickoff prompts, and nothing more. Re-print the whole plan only if it was re-packed, and even then only the changed lines and the window table.

If the limit is close (the user says so, or the tool warns), skip everything else and do steps 4 and 5 first. A good handoff is worth more than a finished task.

## Unfinished tasks

Sometimes the limit hits mid-task anyway. The goal is that the next window starts from a known, working state, and doesn't pay twice for the same mistake.

**1. Save the state, keeping the main branch green.**
- **The code still builds and runs, and the finished part passes its check**: commit it normally with a message such as `T06 (partial): signature parsing done, order creation not started`.
- **The code is broken**: commit the work to a `wip/T06` branch, then return the main branch to the last green commit. The next session can still use the partial work without starting on a broken app.
- **Not a git user, or chat-only**: put the partial code, or a description of it, in the handoff's "Uncommitted or half-done" section. Say exactly which file it belongs in.

**2. Split what's left.** Rename the task: the finished part becomes `T06a` (ticked), and the rest becomes `T06b` with a fresh size and its own done-check. Put `T06b` **first** in the next window. It's now the riskiest task, and the details are freshest.

**3. Decide: continue or restart.** Write the choice into the handoff so the next session doesn't have to work it out:
- **Continue** when the remaining steps are clear and the partial code is sound.
- **Restart with a different approach** when the session was stuck in a debug loop. Write the failed approach under **Gotchas** ("tried X, failed because Y; don't retry"), and give `T06b` a kickoff prompt that names the new approach. Retrying the same thing in a new session usually fails the same way.

**4. Count it fairly.** In the log, an unfinished task counts as **half** its points toward `done`. Counting it as zero would make capacity drop too much. Counting it as full would hide the overrun.

**5. Prevent the next one: late-window rule.** Once most of a window is used (the user says so, `/usage` or `/status` shows it, or the tool warns that the limit is near), only start a task if it is **S**, or if it can be cut short and still leave things working. Otherwise, wrap up early. A finished handoff with unused budget is better than a half-done L.

**6. Unfinished twice? Change tack.** If the same task ends a window unfinished a second time, don't just schedule it again. Pick one of these, tell the user why, and update the plan:
- An **S spike**: a small, throwaway experiment that answers the unknown, such as "does the webhook signature check work in a 20-line script?"
- The **bigger model** for this task only.
- **Smaller scope**: a simpler version that meets the MVP.
- **Park it** under "Later" if the MVP can ship without it.

## Habits that stretch a window

Include the relevant ones in the plan's tips section, and follow them yourself while running tasks. Each one has a reason, because the user needs to know why it saves budget:

- **New conversation per task.** Each message re-sends the whole conversation, so long chats get more expensive with every turn. A fresh chat plus a kickoff prompt is cheaper.
- **Point at files, don't let the agent search.** Listing the 2–4 relevant files beats "look around the codebase".
- **Trim what you paste.** Paste the last 30 lines of an error, not the full 2,000-line log. Paste one screenshot, not five.
- **Do the cheap things yourself.** Installing packages, renaming files, running the dev server, clicking through the UI: these take seconds for a human and real budget for an agent.
- **Stop debugging loops early.** If two attempts at a fix fail, stop. Write what's known into the handoff, and try in a fresh session or with a bigger model. Loops are the biggest window-killer.
- **Commit after every task.** That leaves a safe point to return to and makes the next handoff trivial.
- **Use the cheaper model when the card says `small-ok`**, where the tool allows it.

## Reference files

- `references/sizing.md`: point sizes with examples, default capacity per tool, and the recalibration rule. Read it before packing windows or doing a check-in.
- `references/platforms.md`: notes per tool (how to see remaining usage, model choice, file access, project instructions file). Read it when intake tells you which tool they use.
- `assets/plan-template.md`, `assets/handoff-template.md`: copy and fill these in (agents with file access).
- `assets/chat-plan-template.md`: the compact plan for chat-only users.
