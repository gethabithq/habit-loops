---
name: marimo-notebook
title: marimo Notebook skill
repo: marimo-team/skills
license: Apache-2.0
url: https://gethabit.dev/skills/marimo-team/marimo-notebook
---

# marimo Notebook skill

The marimo notebook skill shows how to write marimo notebooks as Python files: cell structure, script mode, reactivity rules, output rendering, PEP 723 dependencies, marimo check and pytest. For data people who use marimo.

- Install the skill: `npx skills add marimo-team/skills --skill marimo-notebook`
- Source: https://github.com/marimo-team/skills/tree/HEAD/skills/marimo-notebook
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You write a marimo notebook; You convert a script to a notebook; You add tests to a notebook.
Skip it when: You use Jupyter only; You need a plain script.

# Make it a habit: Keep marimo notebooks running clean.

When a marimo notebook changes, your agent runs uvx marimo check, runs the notebook as a script with uv run, runs pytest on test cells if present, and fixes common mistakes like guarded cells, try/except control flow and missing PEP 723 dependencies.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** notebook file changes (event; Claude Code routine or GitHub Actions; `commit touches a marimo notebook .py file`)
- **Verification:** check, run and tests. Hard checks: uvx marimo check reports no issues; uv run <notebook.py> exits 0; pytest <notebook.py> passes when test cells exist; a PEP 723 script header lists dependencies. On fail: retry, max 2 retries.
- **Memory:** notebook check log at `loops/marimo-notebook-check-loop/runs.md`. Read first: issues found before in each notebook.

## Steps

1. **Lint.** Your agent runs uvx marimo check on the notebook.
2. **Run as script.** It runs uv run on the notebook so script mode uses default data.
3. **Check patterns.** It removes if-guards on cells, try/except control flow and cross-cell mutation.
4. **Check outputs.** It makes sure each cell's output is its final expression.
5. **Check dependencies.** It adds a PEP 723 header if missing.
6. **Run tests.** It runs pytest on the notebook when it has test cells.

Stop rule: Stops after 5 notebooks or 2 fix rounds per run.

## Permissions

- Writes: **/*.py, loops/marimo-notebook-check-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/marimo-notebook-check-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: notebook file changes. Verification: check, run and tests. Memory: loops/marimo-notebook-check-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
