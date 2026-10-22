---
name: shadcn-svelte
title: shadcn-svelte skill
repo: huntabyte/shadcn-svelte
license: MIT
url: https://gethabit.dev/skills/huntabyte/shadcn-svelte
---

# shadcn-svelte skill

The shadcn-svelte skill helps agents add, update, fix and compose shadcn-svelte components with the CLI, following rules for forms, styling, icons and composition. For Svelte developers who use components.json.

- Install the skill: `npx skills add huntabyte/shadcn-svelte --skill shadcn-svelte`
- Source: https://github.com/huntabyte/shadcn-svelte/tree/HEAD/skills/shadcn-svelte
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You add components with the CLI; You build forms with Field components; You update registry components.
Skip it when: The project is not Svelte; You use another component library.

# Make it a habit: Keep Svelte UI components current.

Each month your agent reads components.json, runs the shadcn-svelte update command on installed components, reviews the git diff against the skill's composition rules and checks the build. A board keeps conflicts and rule fixes.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** monthly component update (schedule; Claude Code routine; `0 9 1 * *`)
- **Verification:** build and rule checks. Hard checks: build passes; no space-x-* or space-y-* classes in changed files; every Dialog, Sheet and Drawer has a Title; every Avatar has Avatar.Fallback. On fail: notify, max 1 retries.
- **Memory:** component update board at `loops/shadcn-svelte-update-loop/board.md`. Read first: components with custom edits and open conflicts.

## Steps

1. **Read the context.** Your agent reads components.json and lists the aliases.ui folder.
2. **Save local work.** It commits or stashes local changes first.
3. **Update.** It runs npx shadcn-svelte@latest update with --all or per component.
4. **Review the diff.** It reads git diff and resolves conflicts in customized files.
5. **Check the rules.** It checks groups, titles, validation attributes and icon imports against iconLibrary.
6. **Build.** It builds the project and lists open items on the board.

Stop rule: Stops after one update pass and one retry per run.

## Permissions

- Writes: src/lib/components/ui/**, loops/shadcn-svelte-update-loop/**
- Network: shadcn-svelte.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/shadcn-svelte-update-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: monthly component update. Verification: build and rule checks. Memory: loops/shadcn-svelte-update-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
