---
name: shadcn
title: shadcn skill
repo: shadcn-ui/ui
license: MIT
url: https://gethabit.dev/skills/shadcn-ui/shadcn
---

# shadcn skill

shadcn is a skill that adds, searches, fixes, styles and composes shadcn/ui components through the CLI, with project context, docs and strict composition rules. For developers building UI with shadcn/ui.

- Install the skill: `npx skills add shadcn-ui/ui --skill shadcn`
- Source: https://github.com/shadcn-ui/ui/tree/HEAD/skills/shadcn
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: Your project has a components.json; You add or update shadcn components; You build a design system from a DESIGN.md.
Skip it when: You do not use shadcn/ui; You only need plain CSS without components.

# Make it a habit: Components current, local changes kept.

Each week your agent lists installed shadcn components, previews upstream changes with add --dry-run and --diff, merges files with no local changes and asks you before any overwrite. A hard check runs the typecheck and the critical rules. A board keeps pending merges.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly component sync (schedule; Claude Code routine; `0 9 * * 1`)
- **Verification:** typecheck and rules pass. Hard checks: the project typecheck passes; no space-x-* or space-y-* classes in changed files; every Dialog, Sheet and Drawer has a Title; --overwrite was never used without approval. On fail: notify, max 1 retries.
- **Memory:** pending component merges at `loops/shadcn-upstream-sync-loop/board.md`. Read first: components with local changes waiting for a merge decision.

## Steps

1. **Get context.** Run npx shadcn@latest info to get installed components, aliases, base and iconLibrary.
2. **Preview.** For each component run add with --dry-run to list affected files.
3. **Diff.** Run add with --diff per file to compare upstream with local.
4. **Merge.** Take upstream where there are no local changes, and merge by hand where there are.
5. **Ask before overwrite.** Ask the user before using --overwrite on any file.
6. **Review.** Read changed files, check the critical rules and run the typecheck.

Stop rule: Stops after 10 components per run, with at most 1 retry.

## Permissions

- Writes: resolvedPaths.ui folder, loops/shadcn-upstream-sync-loop/**
- Network: ui.shadcn.com
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/shadcn-upstream-sync-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly component sync. Verification: typecheck and rules pass. Memory: loops/shadcn-upstream-sync-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
