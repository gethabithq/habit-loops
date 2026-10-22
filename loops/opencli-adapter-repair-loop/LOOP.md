---
name: opencli-adapter-author
title: OpenCLI Adapter Author skill
repo: jackwener/OpenCLI
license: Apache-2.0
url: https://gethabit.dev/skills/jackwener/opencli-adapter-author
---

# OpenCLI Adapter Author skill

The opencli adapter author skill helps your agent build or improve OpenCLI JS adapters from observed site behavior, existing adapters and browser network evidence, then check and test them. For developers extending OpenCLI with new sites.

- Install the skill: `npx skills add jackwener/OpenCLI --skill opencli-adapter-author`
- Source: https://github.com/jackwener/OpenCLI/tree/HEAD/skills/opencli-adapter-author
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You add a new site to OpenCLI; An adapter broke after a site change; You turn observed requests into a command.
Skip it when: One-off browser clicks; A site adapter already covers the task.

# Make it a habit: Broken site adapters get fixed fast.

Every night your agent runs opencli adapter test on your read adapters. When one fails, it gathers browser and network evidence, repairs the adapter, and re-runs check, test, typecheck and build. It logs failures and fixes per adapter.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** nightly adapter test (schedule; Claude Code routine or cron; `0 3 * * *`)
- **Verification:** check, test, build pass. Hard checks: opencli adapter check passes; opencli adapter test passes for the repaired adapter; typecheck passes; build passes. On fail: retry, max 2 retries.
- **Memory:** adapter failures and fixes at `loops/opencli-adapter-repair-loop/run-log.md`. Read first: adapters that failed recently and why.

## Steps

1. **Test adapters.** Your agent runs opencli adapter test on each read adapter.
2. **Reuse first.** For a failure it checks with opencli list search whether another adapter covers the capability.
3. **Gather evidence.** It opens the site with opencli browser open and reads browser state and network captures.
4. **Repair.** It updates the adapter in clis/<site>/ and returns business data or a typed error with a hint.
5. **Check.** It runs opencli adapter check and opencli adapter test, with --trace retain-on-failure when needed.
6. **Build.** It runs focused tests, typecheck and build for repository changes.
7. **Log.** It writes the failure, the evidence and the fix to the run log.

Stop rule: Stops after 3 repaired adapters per run and 2 retries each; write adapters are never replayed.

## Permissions

- Writes: clis/**, loops/opencli-adapter-repair-loop/**
- Network: the sites the adapters target
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/opencli-adapter-repair-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: nightly adapter test. Verification: check, test, build pass. Memory: loops/opencli-adapter-repair-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
