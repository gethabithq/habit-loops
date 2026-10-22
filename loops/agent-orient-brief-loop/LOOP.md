---
name: indexion-agent-orient
title: Indexion Agent Orient skill
repo: trkbt10/indexion-skills
license: Apache-2.0
url: https://gethabit.dev/skills/trkbt10/indexion-agent-orient
---

# Indexion Agent Orient skill

Indexion agent orient builds a pre-edit structure brief so coding agents learn likely code owners, consumer surfaces and unsafe edit locations before implementing. For teams running coding agents in unfamiliar or large codebases.

- Install the skill: `npx skills add trkbt10/indexion-skills --skill indexion-agent-orient`
- Source: https://github.com/trkbt10/indexion-skills/tree/HEAD/skills/indexion-agent-orient
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: An agent starts in unfamiliar code; You delegate to a subagent; You are unsure which package owns a task.
Skip it when: You know exactly where to edit; Your project does not use indexion.

# Make it a habit: Agents know code owners before editing.

Before each new coding task, your agent runs indexion agent orient to build a structure brief: likely owners, knowledge sources, consumer surfaces and unsafe edit spots. It confirms the owner with doc graph, grep and search, and stops if the edit path is off-limits.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** new coding task starts (event; Claude Code routine; `task.md created or updated`)
- **Verification:** brief + edit gate. Hard checks: indexion agent orient --help succeeds; .indexion/cache/agent/orient.md exists; the intended edit path is not listed under Do Not Implement Here. On fail: stop, max 0 retries.
- **Memory:** orientation map at `.indexion/cache/agent/orient-map.json`. Read first: the prebuilt orientation map, refreshed for changed files only.

## Steps

1. **Check the CLI.** Run indexion agent orient --help and update indexion if the command is missing.
2. **Generate the brief.** Run indexion agent orient with --task-file task.md and write it to .indexion/cache/agent/orient.md.
3. **Read the brief.** Read likely owners, knowledge sources, consumer surfaces, Do Not Implement Here and required preflight.
4. **Confirm the owner.** Run indexion doc graph, indexion grep --semantic and indexion search on the likely owner.
5. **Gate the edit.** Stop and explain if the edit path is off-limits, or gather more evidence if the owner is missing.

Stop rule: Stops after one brief and one owner decision per task.

## Permissions

- Writes: .indexion/cache/agent/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`.indexion/cache/agent/orient-map.json`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: new coding task starts. Verification: brief + edit gate. Memory: .indexion/cache/agent/orient-map.json. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
