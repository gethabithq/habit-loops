---
name: sales-pipeline-coverage-modeling
title: Sales Pipeline Coverage Modeling skill
repo: mbfinotti/sales-skills
license: MIT
url: https://gethabit.dev/skills/mbfinotti/sales-pipeline-coverage-modeling
---

# Sales Pipeline Coverage Modeling skill

The sales pipeline coverage modeling skill helps sales leaders and RevOps set coverage targets from win rates, read raw, weighted and adjusted coverage per segment, find the point of no return and turn gaps into pipeline per rep.

- Install the skill: `npx skills add mbfinotti/sales-skills --skill sales-pipeline-coverage-modeling`
- Source: https://github.com/mbfinotti/sales-skills/tree/HEAD/skills/sales-pipeline-coverage-modeling
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You ask if 3x pipeline is enough; You missed quota despite high coverage; You need new pipeline per rep.
Skip it when: You need to set the quota itself; You want to inspect one deal.

# Make it a habit: Coverage gaps caught by week six.

Every Monday your agent computes raw, weighted and adjusted pipeline coverage per segment, checks timing against each segment's point of no return and runs the gap math per rep. It asks you to approve targets and keeps the model for the next week.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** Mondays at 08:00 (schedule; Claude Code routine; `0 8 * * 1`)
- **Verification:** measurement checks, you approve. Hard checks: every segment target names its method rung and the rate it inverts; raw, weighted and adjusted coverage appear side by side per segment; point of no return uses each segment's own median cycle; seasonal index is own-data or marked as borrowed; deleted rungs are named with the answer that deleted them. On fail: retry, max 2 retries.
- **Memory:** coverage model record at `loops/pipeline-coverage-weekly-loop/model.md`. Read first: per-segment targets, inverted rates, seasonal index and last week's coverage.

## Steps

1. **Fix the quota.** The agent takes the quota as given, or runs sales-quota-setting first if none exists.
2. **Interview.** It asks one question per message about motion, history, calendar and CRM fields.
3. **Pick the method.** It offers raw multiplier, stage-weighted or conversion-inversion with one recommendation for your approval.
4. **Segment targets.** It sets a target per segment and writes the rate it inverts next to it.
5. **Three coverage numbers.** It computes raw, weighted and adjusted coverage, using sales-pipeline-hygiene findings for the adjusted one.
6. **Timing and seasons.** It computes each point of no return and a seasonal index from your own closed-won history.
7. **Gap math.** It turns the deficit into new pipeline per rep and picks a lever.
8. **Record.** It writes governance and stores the approved model.

Stop rule: Stops after one coverage model per run, with at most 2 revision passes.

## Permissions

- Writes: loops/pipeline-coverage-weekly-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/pipeline-coverage-weekly-loop/model.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: Mondays at 08:00. Verification: measurement checks, you approve. Memory: loops/pipeline-coverage-weekly-loop/model.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
