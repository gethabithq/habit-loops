---
name: fix
title: Fix skill
repo: react/react
license: MIT
url: https://gethabit.dev/skills/react/fix
---

# Fix skill

The fix skill has your agent run yarn prettier and yarn linc before a commit and report lint errors that need manual work. For contributors to the React repository who want CI to pass.

- Install the skill: `npx skills add react/react --skill fix`
- Source: https://github.com/react/react/tree/HEAD/.claude/skills/fix
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: you are about to commit; you have lint errors; formatting looks off.
Skip it when: the repo has no yarn linc script; you are not changing code.

# Make it a habit: Commits that pass lint checks.

Before each commit, your agent runs yarn prettier to format changed files, then yarn linc to find lint errors left over. It reports any fixes that need a human hand and logs them, so CI does not fail on style.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** before each commit (event; Claude Code routine; `pre-commit`)
- **Verification:** yarn linc passes. Hard checks: yarn prettier exits cleanly; yarn linc reports zero errors. On fail: notify, max 1 retries.
- **Memory:** manual fixes log at `loops/lint-fix-loop/log.md`. Read first: lint errors that needed manual fixes before.

## Steps

1. **Format.** Run yarn prettier, which formats only the changed files.
2. **Lint.** Run yarn linc to find lint issues that remain.
3. **Report manual fixes.** List every remaining issue that needs a manual fix and log it.

Stop rule: Stops after one format and lint pass per commit, plus one retry.

## Permissions

- Writes: changed files, loops/lint-fix-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/lint-fix-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: before each commit. Verification: yarn linc passes. Memory: loops/lint-fix-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
