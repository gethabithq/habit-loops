---
name: wandb-primary
title: W&B Primary skill
repo: wandb/skills
license: Apache-2.0
url: https://gethabit.dev/skills/wandb/wandb-primary
---

# W&B Primary skill

W&b primary is the main Weights & Biases skill for broad project work: runs and artifacts, Weave traces and evaluations, Reports, Workspaces, Sweeps, Launch and Agent Lens, with fast recipes for large projects.

- Install the skill: `npx skills add wandb/skills --skill wandb-primary`
- Source: https://github.com/wandb/skills/tree/HEAD/skills/wandb-primary
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You ask what happens in a W&B project; You count runs or traces; You compare runs or sweeps.
Skip it when: You do not use W&B; You need one narrow W&B surface only.

# Make it a habit: Daily digest of runs and traces.

Every morning, your agent summarizes a W&B project: run counts by state, recent runs, Weave root traces and error calls, using the skill's fast count recipes. It compares with yesterday and flags crashed runs and new errors.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every morning (schedule; Claude Code routine; `0 8 * * *`)
- **Verification:** counts printed by script. Hard checks: the run count script prints total, finished, crashed and running; calls_query_stats returns a trace count; every number in the digest was printed by a script. On fail: retry, max 1 retries.
- **Memory:** daily project digests at `loops/wandb-project-digest-loop/run-log.md`. Read first: yesterday's run and trace counts.

## Steps

1. **Classify the task.** Treat the digest as a brief task and use one script per surface.
2. **Count runs.** Count runs by state with wandb.Api(timeout=120), per_page=1 and include_sweeps=False.
3. **Count traces.** Use calls_query_stats for total, root and error calls in Weave.
4. **List recent.** Print the five most recent runs and calls.
5. **Compare and log.** Compare with yesterday and write crashed runs and new errors into the log.

Stop rule: Stops after two scripts per surface per run.

## Permissions

- Writes: loops/wandb-project-digest-loop/**
- Network: wandb.ai
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/wandb-project-digest-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every morning. Verification: counts printed by script. Memory: loops/wandb-project-digest-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
