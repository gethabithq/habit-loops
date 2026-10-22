---
name: plannotator-compound
title: Plannotator Compound skill
repo: backnotprop/plannotator
license: Apache-2.0
url: https://gethabit.dev/skills/backnotprop/plannotator-compound
---

# Plannotator Compound skill

Plannotator compound reads a planner's archive of denied plans, sorts the feedback into a taxonomy, and builds an HTML dashboard with corrective prompt instructions. For people who review agent plans and want fewer rewrites.

- Install the skill: `npx skills add backnotprop/plannotator --skill plannotator-compound`
- Source: https://github.com/backnotprop/plannotator/tree/HEAD/apps/skills/extra/plannotator-compound
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: you deny many agent plans; you want your feedback patterns in numbers; you want a prompt fix from your own words.
Skip it when: you have no denied plans yet; you never review agent plans.

# Make it a habit: Fewer denied plans each month.

Once a month your agent reads every denied plan in your Plannotator archive since the last report, finds why you said no, and writes a new versioned HTML report plus corrective prompt instructions. The latest report date sets the cutoff for the next run.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** first day each month (schedule; Claude Code routine; `0 9 1 * *`)
- **Verification:** file counts + your choices. Hard checks: extracted file count matches the denied-file inventory; new report file exists with the next version number; copy button on the prompt block works; every quote comes from a real denied file. On fail: retry, max 1 retries.
- **Memory:** versioned reports and hook at `~/.plannotator/plans/compound-planning-report-v{N}.html`. Read first: the latest report version and its modification date as cutoff.

## Steps

1. **Pick the source.** Use the Plannotator plans folder, or fall back to Claude Code ExitPlanMode denial reasons, or ask you for a folder.
2. **Find last report.** Find the highest compound-planning-report version and ask you whether to run incremental or full.
3. **Count the archive.** Count approved and denied files, the date range and the revision rate, and warn you if fewer than 3 new denials exist.
4. **Extract each denial.** Haiku agents read every in-scope denied file and write structured notes to /tmp/compound-planning/.
5. **Reduce to patterns.** A Sonnet agent builds the denial taxonomy, recurring phrases, evolution over time and numbered prompt instructions.
6. **Build the dashboard.** Write a self-contained HTML report with seven sections in the plans folder under the next version name.
7. **Summarize.** Tell you the top three patterns, the share of denials the instructions cover and where the report lives.
8. **Offer the hook.** Ask whether to write the instructions to enterplanmode-improve-hook.txt, and replace, merge or keep an existing one.

Stop rule: Stops after one report per run; re-launches a failed extraction batch at most once.

## Permissions

- Writes: ~/.plannotator/plans/compound-planning-report*.html, ~/.plannotator/hooks/compound/enterplanmode-improve-hook.txt, /tmp/compound-planning/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`~/.plannotator/plans/compound-planning-report-v{N}.html`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: first day each month. Verification: file counts + your choices. Memory: ~/.plannotator/plans/compound-planning-report-v{N}.html. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
