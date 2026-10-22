---
name: dt-obs-problems
title: DT Obs Problems skill
repo: dynatrace/dynatrace-for-ai
license: Apache-2.0
url: https://gethabit.dev/skills/dynatrace/dt-obs-problems
---

# DT Obs Problems skill

The dt obs problems skill analyses Dynatrace DAVIS problems with DQL: active problem triage, root cause entities, user impact, blast radius and trends, for SRE and operations teams.

- Install the skill: `npx skills add dynatrace/dynatrace-for-ai --skill dt-obs-problems`
- Source: https://github.com/dynatrace/dynatrace-for-ai/tree/HEAD/skills/dt-obs-problems
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: listing active problems; finding the root cause entity; spotting recurring problems.
Skip it when: generic log searching; distributed tracing questions.

# Make it a habit: Active problems triaged every morning.

Every morning, your agent queries dt.davis.problems for active, non-duplicate problems, ranks them by user impact and blast radius, and names the root cause entity. Recurring root causes are compared with the last runs in a log.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every morning (schedule; Claude Code routine; `0 8 * * *`)
- **Verification:** query and list checks. Hard checks: every query filters not(dt.davis.is_duplicate); every query has a time range; status values are ACTIVE or CLOSED, never OPEN; every listed problem has a display_id. On fail: retry, max 2 retries.
- **Memory:** problem triage log at `loops/dynatrace-problem-triage-loop/log.md`. Read first: root causes seen in earlier runs.

## Steps

1. **Fetch active problems.** Your agent runs the standard query on dt.davis.problems with a time range and the duplicate filter.
2. **Rank by impact.** It sorts by dt.davis.affected_users_count and affected entity count.
3. **Find root causes.** It pulls root_cause_entity_name for each problem and resolves names inline.
4. **Check recurrence.** It counts root cause entities over the last 24 hours to spot repeat offenders.
5. **Summarise categories.** It breaks problems down across all categories present, with examples.
6. **Log and recommend.** It writes the ranked list and actions to the log.

Stop rule: Stops after one triage report per run, with at most 20 problems listed.

## Permissions

- Writes: loops/dynatrace-problem-triage-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/dynatrace-problem-triage-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every morning. Verification: query and list checks. Memory: loops/dynatrace-problem-triage-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
