---
name: paperclip-create-plugin
title: Paperclip create plugin skill
repo: paperclipai/paperclip
license: MIT
url: https://gethabit.dev/skills/paperclipai/paperclip-create-plugin
---

# Paperclip create plugin skill

The paperclip create plugin skill scaffolds, installs and verifies external Paperclip plugins with the paperclipai CLI, for developers extending a local Paperclip instance.

- Install the skill: `npx skills add paperclipai/paperclip --skill paperclip-create-plugin`
- Source: https://github.com/paperclipai/paperclip/tree/HEAD/.agents/skills/paperclip-create-plugin
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: starting a new Paperclip plugin; iterating on a local plugin; updating plugin authoring docs.
Skip it when: changing Paperclip core features; publishing to npm only.

# Make it a habit: Plugin builds, tests and installs.

Runs on each change to an external Paperclip plugin. Your agent rebuilds, runs typecheck, tests and build, checks the install status with paperclipai plugin list, and keeps a success checklist for the next run.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** plugin code changed (event; Claude Code routine or GitHub Actions; `push to plugin repository`)
- **Verification:** typecheck, tests, build. Hard checks: pnpm typecheck passes; pnpm test passes; pnpm build passes; plugin status is ready in paperclipai plugin inspect; manifest does not use ctx.assets. On fail: retry, max 2 retries.
- **Memory:** success checklist at `loops/paperclip-plugin-loop/checklist.md`. Read first: last install status, lastError and reload limits.

## Steps

1. **Scaffold if new.** Create the plugin outside Paperclip core with paperclipai plugin init.
2. **Install locally.** Run pnpm install, start pnpm dev and install by absolute path.
3. **Sanity-check package.** Open src/manifest.ts, src/worker.ts and package.json and confirm supported capabilities.
4. **Verify.** Run pnpm typecheck, pnpm test and pnpm build from the plugin folder.
5. **Inspect install.** Read status with paperclipai plugin list and plugin inspect.
6. **Report checklist.** Record scaffold path, commands, install status, test results and reload limits.

Stop rule: Stops after one plugin and 2 fix retries per run.

## Permissions

- Writes: ~/dev/paperclip-plugins/**, loops/paperclip-plugin-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/paperclip-plugin-loop/checklist.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: plugin code changed. Verification: typecheck, tests, build. Memory: loops/paperclip-plugin-loop/checklist.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
