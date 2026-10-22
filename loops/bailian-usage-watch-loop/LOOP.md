---
name: bailian-cli
title: Bailian CLI skill
repo: modelstudioai/cli
license: Apache-2.0
url: https://gethabit.dev/skills/modelstudioai/bailian-cli
---

# Bailian CLI skill

The bailian cli skill teaches your agent to drive the bl command line tool for Aliyun Model Studio: apps, knowledge base search, model lists, usage, quota, monitoring and the skill registry. For teams that build on Bailian.

- Install the skill: `npx skills add modelstudioai/cli --skill bailian-cli`
- Source: https://github.com/modelstudioai/cli/tree/HEAD/skills/bailian-cli
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You call Bailian apps or models; You check Bailian usage or quota; You manage Bailian skills or MCPs.
Skip it when: Plain coding or writing tasks; You do not use Aliyun Bailian.

# Make it a habit: Know your Bailian usage weekly.

Once a week your agent uses the bl CLI to read Bailian usage, quota and model error numbers. It checks that each command ran and compares the numbers with last week, then keeps a short log for the next run.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every Monday morning (schedule; Claude Code routine or cron; `0 8 * * 1`)
- **Verification:** commands ran, numbers logged. Hard checks: the shared bailian-protocol SKILL.md exists before any bl command; bl usage stats exits without an error; bl quota list exits without an error; bl monitor errors exits without an error; this week's row is added to the run log. On fail: notify, max 1 retries.
- **Memory:** weekly usage log at `loops/bailian-usage-watch-loop/run-log.md`. Read first: last week's usage, quota and error numbers.

## Steps

1. **Read the protocol.** Your agent reads the shared bailian-protocol skill first and stops if it is missing.
2. **Check the flags.** It looks up each command in reference/index.md or with bl <command> --help instead of guessing flags.
3. **Read usage.** It runs bl usage stats and bl quota list for the Bailian workspace.
4. **Read errors.** It runs bl monitor errors to see failed model calls.
5. **Compare.** It compares the new numbers with last week's row in the log.
6. **Log and report.** It writes one row to the log and tells you what changed.

Stop rule: Stops after one weekly report with at most 4 bl read commands and 1 retry each.

## Permissions

- Writes: loops/bailian-usage-watch-loop/**
- Network: Aliyun Bailian services via bl
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/bailian-usage-watch-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every Monday morning. Verification: commands ran, numbers logged. Memory: loops/bailian-usage-watch-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
