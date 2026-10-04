# vibe-plus

**Build an app with AI on a $20 plan without hitting the limit halfway through and breaking everything.**

vibe-plus is a free add-on (called a *skill*) for Claude, ChatGPT and other AI coding tools. It turns your app idea into a step-by-step plan, sized so each step fits inside your plan's usage limit.

---

## Sound familiar?

You're building something with Claude Pro or ChatGPT Plus. It's going great… then:

> ⚠️ *"You've reached your usage limit. Your limit resets at 9:40 PM."*

The AI stopped in the middle of a change, so the app is half-broken. When you come back, the AI has forgotten everything, and you spend part of your new allowance explaining the project all over again.

**vibe-plus fixes this:**

| Without vibe-plus | With vibe-plus |
|---|---|
| One huge chat that runs out halfway | Small tasks that each finish well before the limit |
| The app is broken when the limit hits | Every task ends with a working, saved app |
| You re-explain the project every time | A short note tells the AI exactly where you left off |
| Waiting for the limit to reset is dead time | You get a short to-do list for the wait (sign up for accounts, test on your phone) |
| You guess how much fits in one session | It learns how much *you* get done and adjusts the plan |

**You don't need to know how to code.** It's built for people who are learning as they go.

---

## Step 1: Pick your setup

Find the row that matches how you use AI, then follow that section.

| I use… | Go to |
|---|---|
| **Claude** on the website or app (claude.ai) | [Setup A](#setup-a-claude-website-or-app) |
| **ChatGPT** on the website or app (chatgpt.com) | [Setup B](#setup-b-chatgpt-website-or-app) |
| **Claude Code, Codex, Cursor** or another coding tool on my computer | [Setup C](#setup-c-a-coding-tool-on-your-computer) |

Not sure? If you only ever type into a chat box in your browser, you're **A** or **B**.

---

### Setup A: Claude website or app

*Takes about 2 minutes. Do it once.*

1. **Download the skill:** click 👉 [**vibe-plus.skill**](https://github.com/rckycls/vibe-plus/releases/latest/download/vibe-plus.skill). It's saved to your Downloads folder.
2. Open [claude.ai](https://claude.ai) and click your **name or initials** (bottom-left) → **Settings**.
3. Click **Capabilities**.
4. Find **Skills** and click **Upload skill**. If you don't see Skills, first switch on **Code execution and file creation** on the same page.
5. Choose the `vibe-plus.skill` file you downloaded.
   - If it only accepts `.zip` files, rename the file from `vibe-plus.skill` to `vibe-plus.zip` and try again. It's the same file.
6. Make sure the **vibe-plus** switch is **on**.

✅ Done. Jump to [Step 2](#step-2-make-your-plan).

> 💡 **Tip:** make a **Project** in Claude (left sidebar → Projects → New project) for your app, and have all your chats for that app inside it. Projects can store files, so your plan stays in one place.

---

### Setup B: ChatGPT website or app

*Takes about 3 minutes. Do it once.* ChatGPT can't install skills, so you'll give it the instructions as files inside a Project instead.

1. **Download these two files** (right-click each link → **Save link as…**):
   - 👉 [SKILL.md](https://raw.githubusercontent.com/rckycls/vibe-plus/master/skills/vibe-plus/SKILL.md) (the vibe-plus instructions)
   - 👉 [chat-plan-template.md](https://raw.githubusercontent.com/rckycls/vibe-plus/master/skills/vibe-plus/assets/chat-plan-template.md)
2. Open [chatgpt.com](https://chatgpt.com). In the left sidebar, click **New project** and name it after your app (for example *"Recipe app"*).
3. In the project, find **Files** (or **Add files**) and upload both files.
4. Find **Instructions** (sometimes behind the **⋯** menu → *Project settings* or *Instructions*), and paste this:

   ```
   When I ask for a plan, a check-in, or to continue my project, follow the
   vibe-plus instructions in the attached files exactly. I use ChatGPT in the
   browser, so give me plans as text I can save, never as files.
   ```

5. Click **Save**.

✅ Done. Always start your chats **inside this project**. Jump to [Step 2](#step-2-make-your-plan).

---

### Setup C: A coding tool on your computer

*For Claude Code, Codex, Cursor, Gemini CLI and similar. Takes about 1 minute.*

1. Open your **Terminal**:
   - **Mac:** press `Cmd` + `Space`, type **Terminal** and press Enter.
   - **Windows:** press the Windows key, type **PowerShell** and press Enter.
2. Copy this line, paste it into the Terminal, and press **Enter**:

   ```bash
   npx skills add rckycls/vibe-plus -g
   ```

3. If it asks you questions, read them and press **Enter** to accept the suggested answer. If it asks which tools to install for, use the arrow keys and **Space** to tick yours, then press **Enter**.

✅ Done. It now works in every project.

<details>
<summary>It says <code>npx: command not found</code>, or it didn't work</summary>

- `npx` comes with **Node.js**. Install the **LTS** version from [nodejs.org](https://nodejs.org), close and reopen the Terminal, then try step 2 again.
- **Doing it by hand instead:** download [vibe-plus.skill](https://github.com/rckycls/vibe-plus/releases/latest/download/vibe-plus.skill) and unzip it. You get a folder called `vibe-plus`. Move that folder to:
  - **Claude Code:** `~/.claude/skills/` (the `.claude` folder in your home folder)
  - **Codex:** `~/.codex/skills/`
</details>

---

## Step 2: Make your plan

Start a **new chat** and send the message below. Fill in the blanks; rough answers are fine.

- **Setup C, Claude Code:** start the message with `/vibe-plus` instead of "Use vibe-plus".
- **Setup B:** send it inside your ChatGPT project.

```
Use vibe-plus to plan my project.

What I want to build: ___ (e.g. "a website where my family can save recipes")
I'm using: ___ (e.g. "Claude Pro on claude.ai" / "ChatGPT Plus in the browser" / "Claude Code")
Starting from: nothing yet / I already have some code
When I can work on it: ___ (e.g. "2 evenings a week and Saturdays")
My coding experience: ___ (e.g. "none at all")
```

You'll get back:

- 📋 **A plan** split into **windows**. A window is one stretch of AI use before your limit kicks in, about 5 hours on most plans.
- ✅ **Small tasks** for the first window, each with a **ready-to-paste message** (a *kickoff prompt*).
- 🧑 **A short to-do list for you** while the limit resets, things that don't need the AI.
- 📝 **A handoff note.** It's a short "where we left off" summary for the AI.

**Save what it gives you.** On **A** or **B**, copy the plan and the handoff note into your Project (A: *Add content / Files*; B: *Files*). On **C**, the files are saved in your project folder for you.

---

## Step 3: Your routine for each session

Do this every time you sit down to work. It's the same four steps each time.

**1. Start a fresh chat.** On Setup C in Claude Code, type `/clear` instead.

> Why fresh? Every message re-sends the *whole* chat, so long chats burn through your limit faster. Short chats stretch it.

**2. Paste the handoff note, then the next task's kickoff prompt.**
On Setup C you can skip the handoff note, because the tool reads it automatically.

**3. Let the AI work on that one task.** Check it works (each task says how: *"Done when…"*), then start a fresh chat for the next task.

**4. When the session ends, or the limit hits, send:**

```
Use vibe-plus: check-in. I finished ___. I was in the middle of ___. The limit hit: yes / no.
```

It saves your progress and updates your handoff note. It also gives you the **next window's** tasks and prompts, and tells you what to do while you wait.

> 🔁 Then you repeat: wait for the reset, do your 🧑 to-dos, and go back to step 1.

---

## Words you'll see

| Word | What it means |
|---|---|
| **Window** | One stretch of AI use until your limit kicks in (about 5 hours on most $20 plans). |
| **Cooldown** | The wait while your limit resets. vibe-plus gives you useful non-AI jobs for it. |
| **Task size: S / M / L** | Small, Medium, Large. Nothing is ever bigger than L, so no task is too big to finish in one go. |
| **Points** | S = 1, M = 2, L = 4. Each window gets about as many points as you can finish. |
| **Kickoff prompt** | A ready-made message you paste to start one task. |
| **Handoff note** | A short "where we left off" note, so the AI doesn't need everything re-explained. |
| **Check-in** | Telling vibe-plus how the session went, so it can adjust the plan. |
| 🤖 / 🧑 | 🤖 = the AI does it, 🧑 = you do it. |

---

## Questions

<details>
<summary><b>Is it free?</b></summary>

Yes. vibe-plus itself is free. You only need the AI plan you already have.
</details>

<details>
<summary><b>Do I need to know how to code?</b></summary>

No. Tell it you're a beginner and it sizes tasks bigger, explains steps simply, and gives you exact things to click or paste.
</details>

<details>
<summary><b>Does it work on free plans?</b></summary>

Yes, but free limits are much smaller, so you'll get less done per window. vibe-plus adjusts the plan after your first couple of check-ins.
</details>

<details>
<summary><b>The limit hit in the middle of a task. What now?</b></summary>

Send a check-in (Step 3, part 4) and say which task was half done. vibe-plus tells you how to save what's there without breaking your app. It splits the leftover work into a new, smaller task and puts it first next time.
</details>

<details>
<summary><b>It gave me a normal answer instead of a vibe-plus plan.</b></summary>

Make sure your message starts with **"Use vibe-plus"** (or `/vibe-plus` in Claude Code). On Setup A, check the vibe-plus switch is on in Settings → Capabilities. On Setup B, make sure you're chatting inside your project.
</details>

<details>
<summary><b>How do I get updates?</b></summary>

- **Setup A:** download the [latest file](https://github.com/rckycls/vibe-plus/releases/latest/download/vibe-plus.skill) again and re-upload it.
- **Setup B:** download the two files again and replace them in your project.
- **Setup C:** run `npx skills update` in the Terminal.
</details>

<details>
<summary><b>How do I remove it?</b></summary>

- **Setup A:** Settings → Capabilities → Skills → delete vibe-plus.
- **Setup B:** remove the files from your project.
- **Setup C:** run `npx skills remove vibe-plus -g`.
</details>

---

<details>
<summary>For developers: how this repo works</summary>

- The skill itself is in [`skills/vibe-plus/`](skills/vibe-plus/): `SKILL.md`, plus `references/` and `assets/`.
- Test prompts and fixtures are in [`evals/`](evals/).
- **Releasing:** in GitHub, open **Actions → Release skill → Run workflow** and enter a version tag such as `v0.2.0`. You can also publish a release in the GitHub UI or push a `v*` tag. The [release workflow](.github/workflows/release.yml) packages `skills/vibe-plus` into `vibe-plus.skill` and attaches it to the release. `npx skills` users get changes from `master` with `npx skills update`, without needing a release.
</details>
