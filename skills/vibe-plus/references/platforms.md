# Notes per tool

Plans and commands change often. Treat this as a starting point and check the tool's own help (`/help`) when something doesn't match. Don't quote exact message or token numbers to the user as fact; providers change them.

## Common to most entry plans

- Usage resets on a rolling window of about **5 hours** that starts at the first message, not on the clock hour.
- Many plans also have a **weekly cap**.
- Bigger or "thinking" models use up the window much faster than mid-tier ones.
- Chat in a browser and the coding agent often draw from the **same** allowance, so long brainstorming chats eat into coding time.

## Claude Pro: Claude Code (terminal or IDE)

- Instructions file: `CLAUDE.md` at the repo root, loaded automatically each session.
- Remaining usage: `/usage` (or the Usage page in claude.ai settings).
- Fresh context per task: `/clear`. Switch models with `/model`. A mid-tier model is the sensible default on Pro, with the top-tier model for `big` tasks only.
- `/compact` shrinks a long conversation, but a fresh conversation plus a kickoff prompt is usually cheaper and cleaner.

## Claude Pro: claude.ai (browser or app)

- Chat-only: no file writes. Use the chat-only output path.
- Put `PLAN.md` and the latest handoff into a **Project** as project knowledge so every new chat in it sees them.
- Usage: Settings → Usage.

## ChatGPT Plus: Codex (CLI, IDE extension, or cloud)

- Instructions file: `AGENTS.md` at the repo root.
- Remaining usage: `/status` in the Codex CLI, or the usage page in ChatGPT settings.
- Start a fresh conversation per task (`/new` in the CLI, or a new task in the cloud UI). Choose models with `/model`.
- Cloud tasks run in parallel. That's handy, but each one draws budget, so don't fire off several speculative tasks.

## ChatGPT Plus: chatgpt.com (browser or app)

- Chat-only. Use **Projects** to keep `PLAN.md` and the handoff as project files.

## Gemini (Gemini CLI, Google AI plans)

- Instructions file: `GEMINI.md`. `/stats` shows session usage. Use `/clear` between tasks.

## Cursor or GitHub Copilot paid tiers

- These limits are often **monthly** request or credit pools rather than 5-hour windows. The plan still helps: treat a "window" as one focused work session, and use the weekly-cap logic to spread the pool across the month.
- Instructions: `AGENTS.md`, `.cursor/rules/` (Cursor), or `.github/copilot-instructions.md` (Copilot).

## Unknown tool

Ask which file the tool reads automatically for project instructions. If there isn't one, rely on the user pasting the handoff block at the start of each session.
