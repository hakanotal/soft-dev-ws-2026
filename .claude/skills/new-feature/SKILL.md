---
name: new-feature
description: Build a new feature in its own git worktree, following the project's guardrails and conventions
argument-hint: <feature description>
disable-model-invocation: true
---

# New Feature: $ARGUMENTS

## Context

Recent commits:
!`git log --oneline -5`

Uncommitted changes:
!`git status --short`

Current branch: !`git branch --show-current`

## Task

Implement the feature described below with strict adherence to the project's conventions and guardrails.

**Feature description:** $ARGUMENTS

## Guardrails

0. **Never use em dashes** in any text you write: product copy, comments, docs or commit messages. Use a comma, a colon, brackets or a full stop. See `CLAUDE.md`.
1. **Read before write.** Read `CLAUDE.md` and every file you are about to change before editing it.
2. **No new dependencies** unless necessary. Check `pyproject.toml` and `web/package.json` first. If a new dependency is needed, justify it and confirm the package exists on pypi.org or npmjs.com.
3. **Follow existing patterns.** Look at neighbouring files for code style, naming, imports, and structure. Mimic them exactly.
4. **No comments** unless explicitly asked.
5. **Never read, print or copy `.env`.**

## Workflow

### 1. Isolate with a worktree

Work in a dedicated git worktree so other agents can keep working on `main` in parallel.

Pick a short kebab-case slug of two to four words from the feature description (for example `species-summary`). If a branch with that name already exists (`git branch --list "feature/<slug>"`), pick another.

```bash
SLUG="<slug>"
MAIN_ROOT="$(git rev-parse --show-toplevel)"
BRANCH="feature/${SLUG}"
WORKTREE="${MAIN_ROOT}/.claude/worktrees/${SLUG}"
git worktree add -b "${BRANCH}" "${WORKTREE}" main
echo "MAIN_ROOT=${MAIN_ROOT} BRANCH=${BRANCH} WORKTREE=${WORKTREE}"
```

Each Bash call starts a fresh shell, so these variables do not survive. Note the three printed values and use them literally in every later step.

Install dependencies in the worktree, because `.venv` and `node_modules` are not shared between worktrees. Skip a line if its project file (`pyproject.toml` or `web/package.json`) does not exist yet:

```bash
cd "<WORKTREE>" && uv sync
cd "<WORKTREE>" && npm --prefix web install
```

All later work happens inside `<WORKTREE>`. **Never edit files in `<MAIN_ROOT>`.**

### 2. Understand the codebase

Inside the worktree:

1. Read `CLAUDE.md`.
2. Search the codebase to locate files relevant to the feature.
3. Read neighbouring files to understand code style, naming, imports, and structure.

### 3. Plan

List every file to create or edit, the tests you will add, and any config or env var changes. Flag dependencies or trade-offs.

**Present the plan and wait for the user's go-ahead before editing anything.**

### 4. Implement

Apply changes inside the worktree, following existing conventions exactly. Add or update tests in `tests/` for any logic in `analysis/`. If the analysis output changed, regenerate it with `uv run python -m analysis.analyze`.

### 5. Verify

Run the check command from `CLAUDE.md` inside the worktree:

```bash
cd "<WORKTREE>" && uv run pytest && npm --prefix web run build
```

Fix any failures before going on. Then tell the user exactly how to see the feature working (for example `cd "<WORKTREE>" && npm --prefix web run dev`, then what to click).

### 6. Commit

```bash
git -C "<WORKTREE>" add -A
git -C "<WORKTREE>" commit -m "<short imperative subject, e.g. Add species summary table>"
```

### 7. Merge back (requires user confirmation)

**Do NOT merge automatically.** Present a summary and wait for explicit confirmation.

Once the user confirms, check that the main checkout is on `main` with no uncommitted changes, then merge:

```bash
git -C "<MAIN_ROOT>" branch --show-current
git -C "<MAIN_ROOT>" status --short
git -C "<MAIN_ROOT>" merge --no-ff "<BRANCH>" -m "Merge <BRANCH>"
```

If the merge has conflicts, resolve them in `<MAIN_ROOT>`, run the check command there, and ask the user to confirm again before committing.

### 8. Clean up the worktree

After a successful merge:

```bash
git -C "<MAIN_ROOT>" worktree remove "<WORKTREE>"
git -C "<MAIN_ROOT>" branch -d "<BRANCH>"
```

If the user declines the merge, leave the worktree intact and report its path so they can inspect it.

## Output

- List every file created or modified.
- Note any env vars or config changes needed.
- Flag any trade-offs or deferred items.
- State the worktree path and branch name.
