# Compact plan for chat-only users

Use this shape when the user works in a browser chat (claude.ai, chatgpt.com) with no file access. Every line counts against their limit, so keep the whole reply under about 150 lines. Below is the reply's skeleton; replace the `<...>` parts.

---

<1–2 lines: what you planned and how many windows it takes.>

**Save this as `PLAN.md` in your Project:**

````markdown
# <Project>: vibe-plus plan
**Tool:** <ChatGPT Plus, browser> · **Capacity:** <N> pts/window · **Availability:** <...>

## Decisions (locked)
- <stack, libs, structure, storage, how they run it: 4–6 bullets>

## MVP / Later
- MVP: <one line> · Later: <one line>

## Assumptions
- <only the ones that change the plan>

## Windows
| Window | Tasks | Pts | Cooldown 🧑 |
|---|---|---|---|
| W1 | T01, T02 | 5 | H01 ... |
| W2 | T03, T04, T05 | 5 | H02 ... |

## Tasks (full cards arrive at each window's start)
- [ ] T01 · L · <title> · done when <check>
- [ ] T02 · S · <title> · done when <check>
- [ ] T03 · M · <title> · done when <check>
- [ ] H01 🧑 <title> (<~minutes>)

## Log
| Date | Window | Planned | Done | Limit hit | Notes |
|---|---|---|---|---|---|
````

**Project instructions** (paste once into the Project's instructions, so prompts don't need to repeat them):
> <3–5 lines: stack reminder; "I paste the current files you need; return changed files in full"; "if two fixes fail, stop and give me a 5-line note for HANDOFF"; never ask for secrets>

**Starter handoff** (paste at the top of each new chat, and update it at each check-in):
```
HANDOFF · W1 · capacity <N>
Done: nothing yet
Next: T01 <title>
Gotchas: none
Waiting on me: <H01 ...>
```

**W1, full cards:**

**T01 · <title>** `L`: <goal in one line> · Files: `<...>` · Done when: <check>
```
<kickoff prompt: task-specific only, 3–6 lines; shared rules live in the Project instructions>
```

**T02 · <title>** `S`: ...

**Right now:** <1–3 steps>. **Cooldown after W1:** <🧑 tasks>.
**At the end of W1**, send `check-in: W1, done T01+T02, limit hit y/n` in a fresh chat. You'll get the updated handoff and W2's prompts.
**Fresh chat per task.** Every message re-sends the whole chat, so short chats stretch your limit.
