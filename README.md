# AI-Assisted Software Development Workshop

Starter repo for the workshop. During the day you will use Cursor and Claude Code to build **Penguin Data Explorer**: a Python analysis of the Palmer Penguins dataset with a simple web page on top, published on GitHub Pages so you leave with a live URL.

## Before the workshop

**Follow [docs/install.md](docs/install.md)**, starting at step 1, even if you have nothing installed yet. It ends with a check that tells you whether you are ready.

## What is in here

| Path | What it is |
|---|---|
| `CLAUDE.md` | Instructions Claude Code (and Cursor) read at the start of every session: stack, commands, rules |
| `data/penguins.csv` | The dataset. See `data/README.md` for the columns |
| `docs/install.md` | Setup guide |
| `docs/cheatsheet.md` | Shortcuts and commands for the day |
| `.claude/settings.json` | Shared Claude Code settings. Blocks reading `.env` |
| `.claude/skills/new-feature/` | The `/new-feature` skill |
| `.mcp.json` | MCP servers for Claude Code: Context7 (library docs) and Playwright (browser) |
| `.github/workflows/deploy.yml` | Publishes `web/` to GitHub Pages |
| `.env.example` | Names of environment variables. Copy to `.env` for real values |

The `analysis/` and `web/` folders do not exist yet. You will build them with Claude during the workshop.
