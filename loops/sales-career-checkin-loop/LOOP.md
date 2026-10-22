---
name: sales-career
title: Sales Career skill
repo: mbfinotti/sales-skills
license: MIT
url: https://gethabit.dev/skills/mbfinotti/sales-career
---

# Sales Career skill

The sales career skill coaches one candidate through entering sales, moving from SDR to AE and choosing the next step, with interview prep, an evidence audit, skill-gap roadmaps and offer checks, for B2B SaaS and B2C sales.

- Install the skill: `npx skills add mbfinotti/sales-skills --skill sales-career`
- Source: https://github.com/mbfinotti/sales-skills/tree/HEAD/skills/sales-career
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You want to break into tech sales; You prepare for an SDR interview; You want to judge a sales offer.
Skip it when: You are hiring reps; You need help with one live deal.

# Make it a habit: Your career plan stays on track.

Each week your agent reloads your sales career roadmap, compares your funnel numbers and milestones with the plan, and re-runs the path choice after 4 to 6 weeks without movement. You confirm every change, and it keeps the roadmap and evidence bank.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** Sundays at 18:00 (schedule; Claude Code routine; `0 18 * * 0`)
- **Verification:** quality gate 8/8, you pick. Hard checks: quality gate scores 8 of 8; evidence audit passes for 100% of claims; the path was picked explicitly by you from 2 to 3 options; every milestone has a date and an exit trigger. On fail: retry, max 2 retries.
- **Memory:** roadmap and evidence bank at `loops/sales-career-checkin-loop/roadmap.md`. Read first: chosen path, milestone dates, audited evidence and benchmark snapshot.

## Steps

1. **Interview.** On the first run the agent asks one question per message about your role, target, date and runway.
2. **Diagnose.** It places you on the entry or promotion ladder using the dated benchmarks.
3. **Weigh paths.** It presents 2 to 3 paths with trade-offs and waits for your explicit pick.
4. **Build the roadmap.** It fills references/career-roadmap-template.md section by section, checking each with you.
5. **Audit evidence.** It checks every number for arithmetic, provenance and depth, and reframes what fails.
6. **Weekly check-in.** It compares screen, role-play and offer rates with the milestones.
7. **Re-route.** After 4 to 6 weeks without movement it re-runs the path step.

Stop rule: Stops after one check-in per run, with at most 2 fix passes on the quality gate.

## Permissions

- Writes: loops/sales-career-checkin-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/sales-career-checkin-loop/roadmap.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: Sundays at 18:00. Verification: quality gate 8/8, you pick. Memory: loops/sales-career-checkin-loop/roadmap.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
