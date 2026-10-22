---
name: nx-workspace
title: Nx Workspace skill
repo: nrwl/nx-ai-agents-config
license: MIT
url: https://gethabit.dev/skills/nrwl/nx-workspace
---

# Nx Workspace skill

The nx workspace skill helps your agent explore an Nx monorepo read-only: list and filter projects, read full resolved targets, check nx.json and query the project graph, for teams who work in Nx workspaces.

- Install the skill: `npx skills add nrwl/nx-ai-agents-config --skill nx-workspace`
- Source: https://github.com/nrwl/nx-ai-agents-config/tree/HEAD/artifacts/skills/nx-workspace
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You need to know what is in a monorepo; You look up how to build or test a project; You want to see what depends on a library.
Skip it when: The repo does not use Nx; You want to change config, not read it.

# Make it a habit: A current map of your monorepo.

Every week your agent reads the Nx workspace with nx show projects --json, nx show project --json and nx graph --print, then writes a map of projects, targets and dependencies. It compares the map with last week's and notes what changed.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every Monday (schedule; Claude Code routine or cron; `0 7 * * 1`)
- **Verification:** counts match the graph. Hard checks: nx show projects --json | jq 'length' is above zero; every listed project appears in nx graph --print nodes; map file exists with targets for each project. On fail: notify, max 1 retries.
- **Memory:** last workspace map at `loops/nx-workspace-map-loop/map.md`. Read first: last week's projects, targets and dependency edges.

## Steps

1. **Pick the runner.** Your agent checks the lockfile to know whether to prefix nx with npx, pnpx or yarn.
2. **List projects.** It runs nx show projects --json and counts them with jq.
3. **Read targets.** For each project it runs nx show project <name> --json instead of reading project.json.
4. **Read the graph.** It runs nx graph --print to collect dependency edges.
5. **Read nx.json.** It notes targetDefaults, namedInputs and plugins.
6. **Diff and write.** It compares with the last map and writes new projects, removed targets and new edges.

Stop rule: Stops after one workspace map per run.

## Permissions

- Writes: loops/nx-workspace-map-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/nx-workspace-map-loop/map.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every Monday. Verification: counts match the graph. Memory: loops/nx-workspace-map-loop/map.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
