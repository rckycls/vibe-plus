# vibe-plus

An agent skill for people building with AI on **entry-level plans**: Claude Pro, ChatGPT Plus / Codex, Gemini, Cursor or Copilot paid tiers, and similar. It helps you get the most out of every usage window.

vibe-plus plans your project, splits it into tasks that each fit inside one usage window, and packs those tasks into windows. It also keeps a short handoff file so each new session starts cheaply, and moves non-AI chores into the cooldown while your limit resets.

## What it does

- **New plan:** asks a few questions in one go, locks the stack and scope, and breaks the work into S/M/L tasks. Each task has a goal, the files it touches, a done-check, and a ready-to-paste kickoff prompt. Tasks are packed into windows with the riskiest work first and wrap-up time reserved.
- **Resume:** reads `vibe-plus/HANDOFF.md` instead of re-exploring your repo and starts the next task.
- **Check-in:** logs what got done, learns your real per-window capacity, and re-plans the rest.

It writes two files to your project: `vibe-plus/PLAN.md` and `vibe-plus/HANDOFF.md`. If your tool is chat-only, it gives you markdown to save in a Project instead.

## Install

The skill lives in [`skills/vibe-plus/`](skills/vibe-plus/).

| Tool | How |
|------|-----|
| Claude Code | Copy `skills/vibe-plus` to `~/.claude/skills/vibe-plus` (all projects) or `.claude/skills/vibe-plus` (one project) |
| Codex CLI | Copy `skills/vibe-plus` to `~/.codex/skills/vibe-plus` |
| claude.ai | Zip the `vibe-plus` folder and upload it under Settings → Capabilities → Skills |
| Others | Paste `SKILL.md` into your project's custom instructions, or ask your agent to read it |

## Use

- "I'm on Claude Pro and want to build a habit-tracker app. Plan it with vibe-plus."
- "Resume my vibe-plus plan."
- "Hit my limit, log progress and re-plan."
