Your list covers the tooling well. What it's missing is mostly what makes vibecoding reliable: a mental model of how the agent works, project memory files, verification, and safety. I'd also move git to before any AI tool. Git is the undo button, and it's what makes it safe to let an agent edit freely.

## What I'd add

**How agents work (20 min opener).** Cover the agent loop (read files, plan, edit, run commands, check results), what the context window is, why long sessions get worse, and why models confidently make up APIs. Once people see this, Context7, /clear and plan mode all make sense.

**Project memory: CLAUDE.md and Cursor rules.** Run /init, then edit the file by hand: the stack, how to run tests, conventions, files not to touch. This is the habit that pays off most, and it's not on your list yet.

**Checking the work.** The agent writes and runs tests, people read diffs before accepting them, and they run the app themselves. A rule worth teaching: the AI isn't done until it has shown you something working.

**Recovery.** Checkpoints and rewind in Claude Code (Esc twice or /rewind), git restore, and a commit after every step that works. Break something on purpose during the demo and recover from it. People remember that part.

**Managing context.** Use /clear between tasks, /compact for long sessions, start fresh sessions, and keep each task small.

**Security and secrets.** Cover .env with .gitignore, an .env.example file, and deny rules so the agent can't read secrets. Explain the risk of --dangerously-skip-permissions and of prompt injection through web pages and MCP servers. Show people how to check that a package the AI suggests actually exists. If your group works with research or student data, also cover what university policy allows them to send to a cloud model.

**Terminal basics.** cd, ls, running scripts, and package managers (Homebrew, npm, uv). A lot of what feels like vibecoding trouble is really terminal trouble.

**Shipping.** Deploy the final project to GitHub Pages or Vercel so everyone leaves with a live URL. Pull requests with AI review (Claude's GitHub integration or Cursor's Bugbot) fit here too.

**Optional advanced topics.** Hooks (for example, auto-formatting after every edit), subagents (a reviewer agent), custom slash commands and plugins. One quick demo of each is enough.

## Suggested flow

This assumes one full day. It splits cleanly into two half days.

| Block | Content | Time |
|---|---|---|
| 0. Pre-work | Install Cursor, git, Node or Python, Claude Code; create a GitHub account and log in to everything. Send a checklist with commands to verify each install. | Before the day |
| 1. How agents work | The agent loop, context, how agents fail, vibecoding vs. AI-assisted engineering | 20 min |
| 2. Terminal, git, GitHub | Repos, commits, branches, push, .gitignore, PRs | 60 min |
| 3. Cursor | Tour, extensions, inline edit vs. agent, rules | 30 min |
| 4. Claude Code core | Sessions, CLAUDE.md, plan mode then accept edits, permissions, rewind, context commands | 60 min |
| 5. Environments and secrets | venv/uv or npm, .env, deny rules | 20 min |
| 6. Extending | MCP servers (Context7; Playwright so the agent can see the browser; GitHub), a custom skill, one hook | 45 min |
| 7. Worktrees | Two agents building two features in parallel, then merge | 30 min |
| 8. Final project | Spec, plan, small build loops, tests, commit, PR, deploy | 90 to 120 min |
| 9. Wrap-up | Pitfalls, costs and plans, cheat sheet | 15 min |

## How to teach it

**Make installation homework.** Installing during the session eats the first hour, and anyone who hits an error stays behind for the rest of the day. Have a backup such as GitHub Codespaces for anyone whose install fails.

**Hand out a starter repo** with CLAUDE.md, .cursor/rules, .mcp.json, .gitignore and .env.example already set up. From block 4 onward, build the final project inside that same repo instead of making separate toy demos. Each concept then gets used right away on something real.

**Pick one main agent.** Cursor's agent and Claude Code both have plan modes, rules and MCP, and teaching both side by side confuses beginners. I'd use Cursor as the editor and diff viewer, run Claude Code through its Cursor extension as the agent, and mention that Cursor's own agent works much the same way.

**Use "I do, we do, you do."** Demo it, do it together, then give a short solo exercise. Pair people up for the final project.

**Choose a small, visual project the group cares about.** If your group is academic, a reading-list tracker works well: it imports a BibTeX file, shows a searchable table and deploys to GitHub Pages. It covers file parsing, UI, tests and docs lookup without needing a backend.

**Recheck install commands and feature names the day before.** Both tools change often.

If you tell me how long the workshop is and how technical the group is, I can tighten the timings and turn this into a slide deck or a handout.