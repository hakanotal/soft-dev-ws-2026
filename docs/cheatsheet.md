# Cheat sheet

Where a shortcut differs, it is written as **Windows / Linux** then **macOS**.

## Cursor

| Do this | Press |
|---|---|
| Command Palette (find any command) | Ctrl+Shift+P / Cmd+Shift+P |
| Open or close the terminal | Ctrl+\` (all systems) |
| Preview a Markdown file | Ctrl+Shift+V / Cmd+Shift+V |
| Extensions panel | Ctrl+Shift+X / Cmd+Shift+X |
| Find a file by name | Ctrl+P / Cmd+P |
| Open Claude Code in the editor | Click the Spark icon, or Command Palette > *Claude Code: Open in New Tab* |

## Claude Code: starting and stopping

| Command | What it does |
|---|---|
| `claude` | Start a session in the current folder |
| `claude -c` | Continue your last session |
| `/resume` | Pick an older session to continue |
| `/exit` | Quit |
| **Esc** | Stop Claude mid-task (keeps what it already did) |
| **Esc Esc** or `/rewind` | Go back to an earlier point and undo Claude's file edits |

## Claude Code: typing

| Do this | Press |
|---|---|
| New line in your message | Ctrl+J (always works), or Shift+Enter after running `/terminal-setup` once |
| Point Claude at a file | Type `@` and the file name, for example `@data/README.md` |
| Paste a screenshot | Alt+V on Windows, Ctrl+V on macOS and Linux |

## Modes and permissions

- **Shift+Tab** cycles the mode: *manual* (asks before edits) > *accept edits* > *plan* (reads and plans, changes nothing). Start big tasks in plan mode, read the plan, then switch to accept edits.
- `/permissions` shows what Claude may do without asking. This repo blocks it from reading `.env` (see `.claude/settings.json`).
- Never use `--dangerously-skip-permissions` on your own computer. It lets Claude run anything without asking.

## Context: keep sessions sharp

| Command | When |
|---|---|
| `/clear` | Between unrelated tasks. Fresh context, same folder |
| `/compact` | A long session is getting slow or forgetful |
| `/context` | See what is filling the context window |
| `/usage` | See how much of your plan you have used |
| `/init` | Create or refresh `CLAUDE.md` from the code |
| `/memory` | Edit `CLAUDE.md` and other memory files |

One task per session, small steps, and `/clear` when you switch topics.

## Git: your undo button

Rewind only undoes Claude's file edits. It does **not** undo commands Claude ran (deleting files, installing packages). Commit every time something works.

```
git status                      # what changed?
git diff                        # show the changes line by line
git add -A                      # stage everything
git commit -m "Add species chart"
git restore path/to/file        # throw away changes to one file
git log --oneline               # history
git switch -c my-feature        # new branch
git push                        # send commits to GitHub
```

## This project

```
uv sync                             # install Python dependencies
uv run python -m analysis.analyze   # regenerate web/public/data/summary.json
uv run pytest                       # Python tests
npm --prefix web install            # install web dependencies
npm --prefix web run dev            # run the web page locally
npm --prefix web run build          # build for deployment
```

**Deploy:** on GitHub, open your repo's *Settings > Pages* and set *Source* to **GitHub Actions** (once). After that, every push to `main` that changes `web/` publishes the site. The address appears under *Settings > Pages* and in the *Actions* tab.

## Extending Claude Code

- **MCP servers** (`/mcp`): this repo ships two in `.mcp.json`. *context7* fetches current library docs ("use context7 to check the pandas docs for groupby"). *playwright* lets Claude open the web page and look at it.
- **Skills:** `/new-feature <description>` builds a feature in its own git worktree, following the rules in `.claude/skills/new-feature/SKILL.md`.
- **Worktrees:** `claude -w <name>` starts a session in a separate copy of the repo, so two agents can work in parallel.
- **Hooks** run a command automatically. Example for `.claude/settings.json`, which formats Python after every edit and works on every system:
  ```json
  "hooks": {
    "PostToolUse": [
      { "matcher": "Edit|Write", "hooks": [ { "type": "command", "command": "uvx ruff format ." } ] }
    ]
  }
  ```

## Staying safe

- Secrets go in `.env` (never committed). Variable names go in `.env.example`.
- Before installing a package Claude suggests, check that it exists and is the real one: `https://pypi.org/project/<name>` or `https://www.npmjs.com/package/<name>`. Models sometimes invent package names.
- Web pages, files and MCP servers can contain instructions aimed at Claude (prompt injection). Read what it is about to run.
- Check your institution's policy before giving a cloud model student, patient or research participant data.
- The rule for the day: **the AI is not done until it has shown you something working.**
