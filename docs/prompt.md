
# One-shot build prompt

Paste this into Claude Code to build the first working version of Penguin Data Explorer in one go, using the `/new-feature` skill.

## Before you paste

1. Commit everything on `main`. The skill creates its worktree from `main`, so uncommitted changes will not be in it.
2. In Cursor's terminal, from the repo root, run `claude`.
3. Approve the **context7** and **playwright** MCP servers if asked. Google Chrome must be installed, because Playwright uses it.

## The prompt

Copy everything in the box and paste it as one message.

```text
/new-feature Build the first version of Penguin Data Explorer from data/penguins.csv, following CLAUDE.md. Scaffold both halves exactly as its Status section describes, then build the following.

Analysis (Python, in analysis/):
1. load_penguins(path): read the CSV and treat "NA" as missing.
2. overview(df): number of rows, number of species, number of islands, and missing values per column.
3. species_summary(df): for each species, the count and the mean bill length, bill depth, flipper length and body mass, ignoring missing values, rounded to 1 decimal.
4. island_counts(df): penguins per island, split by species.
5. scatter_points(df): species, flipper_length_mm and body_mass_g for every row where both measurements are present.
6. analyze.py runs all of these and writes a single file, web/public/data/summary.json.
Test every function in tests/ with small hand-made DataFrames, including at least one case with missing values.

Web page (Vite, vanilla JavaScript, in web/):
- Replace the Vite starter page completely.
- A header with the title "Penguin Data Explorer" and a one-line credit to the Palmer Penguins dataset (see data/README.md).
- Four overview cards: total penguins, species, islands, missing values.
- The species summary as a table that sorts when you click a column header.
- A bar chart of penguins per island, split by species.
- A scatter plot of flipper length against body mass, coloured by species, with a legend and buttons to show or hide each species.
- Draw both charts as inline SVG with plain JavaScript. Do not add a chart library or any dependency beyond the ones CLAUDE.md lists.
- Load all data from ./data/summary.json. The page must be readable on a phone screen.

Done means: the check command passes, summary.json is regenerated, and you have started the dev server in the background, opened the page with the Playwright MCP server, taken a screenshot, and confirmed the browser console shows no errors. Before asking to merge, tell me what the page shows and where the screenshot is saved.
```

## What happens

1. Claude creates a worktree in `.claude/worktrees/<slug>` on a `feature/<slug>` branch.
2. It stops and shows a plan. Read it, then reply `go ahead` (or ask for changes). This is the plan, then build habit.
3. It scaffolds, builds, runs the check command, opens the page in Chrome and reports back.
4. It stops again before merging. Look at the page yourself first: `npm --prefix .claude/worktrees/<slug>/web run dev`, then open the address it prints. Reply `merge` when you are happy.

## After the merge

1. On GitHub, open the repo's **Settings > Pages** and set **Source** to **GitHub Actions** (once per repo, before the first push of `web/`).
2. Run `git push`.
3. Watch the **Actions** tab. When the run is green, the site address appears under **Settings > Pages**.
