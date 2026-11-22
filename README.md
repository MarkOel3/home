# Home Repo

A shared starting point for working with Claude Code. Cloning this repo gives you:

- **A curated set of skills** (in `.claude/skills/`), available whenever you run Claude from inside this repo
- **A status line** that shows how much of the context window you've used
- **Lean Claude settings** that turn off features we don't use, so each session starts with less context

## Setup

It takes about 5 minutes. Run the steps in order.

### 1. Install the Claude Code CLI

Follow the official quickstart: https://code.claude.com/docs/en/quickstart

Check that it worked:

```bash
claude --version
```

### 2. Clone this repo

```bash
git clone <repo-url> ~/Repos/home
cd ~/Repos/home
```

Skills load only when you start `claude` from inside this folder (or a subfolder).

### 3. Install the shared settings and status line

> ⚠️ **These commands overwrite your existing files.** If you already have a `~/.claude/settings.json` you want to keep, back it up first (the commands below do this for you) and merge your changes back in afterwards.

From inside the repo folder:

```bash
# Back up existing files, if there are any
[ -f ~/.claude/settings.json ] && cp ~/.claude/settings.json ~/.claude/settings.json.bak
[ -f ~/.config/ccstatusline/settings.json ] && cp ~/.config/ccstatusline/settings.json ~/.config/ccstatusline/settings.json.bak

# Copy the shared settings
mkdir -p ~/.claude ~/.config/ccstatusline
cp settings.json ~/.claude/settings.json
cp ccstatusline/settings.json ~/.config/ccstatusline/settings.json
```

What this gives you:

- **`~/.claude/settings.json`**: turns on the status line and turns off auto memory, feedback surveys, and unused built-in tools and skills, so sessions start with a smaller context.
- **`~/.config/ccstatusline/settings.json`**: sets the layout of the status line, including context length.

The status line runs through `npx`, so you need [Node.js](https://nodejs.org/) installed.

### 4. Start Claude and connect your issue tracker

```bash
claude
```

Then, at the Claude prompt, run:

```
/setup-matt-pocock-skills
```

and follow the prompts to connect your issue tracker (e.g. GitHub).

### 5. Check that auto memory is off

Step 3 should already have turned it off. To confirm, run `/memory` inside Claude and make sure auto memory is off.

### ✅ Done

When you restart `claude` in this repo, the status line should appear at the bottom. Type `/` to see the available skills.

---

## Managing skills

Run these commands from the repo root. Skill versions are tracked in `skills-lock.json`, so commit any changes so your colleagues get them too.

| Task | Command |
| --- | --- |
| List installed skills and see whether they're up to date | `npx skills@latest list` |
| Add skills from a source | `npx skills@latest add mattpocock/skills -a claude-code` |
| Update all skills | `npx skills@latest update` |
| Update specific skills | `npx skills@latest update tdd grilling` |
| Remove a skill | `npx skills@latest remove wizard` |

## Troubleshooting

- **Skills don't appear when I type `/`.** Make sure you started `claude` from inside this repo.
- **No status line.** Check that `~/.claude/settings.json` was copied (step 3), that Node.js is installed, and then restart `claude`.
- **I lost my own Claude settings.** Restore them from `~/.claude/settings.json.bak` and merge in the keys you want from this repo's `settings.json`.
