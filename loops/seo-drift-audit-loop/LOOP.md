---
name: seo
title: Claude SEO skill
repo: agricidaniel/claude-seo
license: MIT
url: https://gethabit.dev/skills/agricidaniel/seo
---

# Claude SEO skill

The claude seo skill is a hub for SEO work: full site audits, technical SEO, schema, Core Web Vitals, E-E-A-T, sitemaps, local SEO, GEO for AI answers and drift monitoring, run through /seo commands. For site owners and SEO teams.

- Install the skill: `npx skills add agricidaniel/claude-seo --skill seo`
- Source: https://github.com/agricidaniel/claude-seo/tree/HEAD/skills/seo
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You want a full site audit; You track SEO changes over time; You check schema or Core Web Vitals.
Skip it when: You need paid ads advice; You have no website yet.

# Make it a habit: Catch SEO drops every week.

Every Monday your agent runs /seo drift compare against the stored baseline of your site, then a /seo technical pass on what changed. Findings land in Critical, High, Medium and Low with a failure check each, and the drift history is the memory.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every Monday morning (schedule; Claude Code routine; `0 6 * * 1`)
- **Verification:** doctor, baseline and report. Hard checks: claude-seo doctor --json reports the runtime ready; a drift baseline exists for the URL; the report gives a SEO Health Score from 0 to 100; every recommendation names how we would know it failed; Core Web Vitals use INP, never FID. On fail: notify, max 1 retries.
- **Memory:** drift history at `loops/seo-drift-audit-loop/history.md`. Read first: the output of /seo drift history and last week's open findings.

## Steps

1. **Check the runtime.** Run the claude-seo doctor --json check and suggest /seo setup if it is not ready.
2. **Read history.** Run /seo drift history for the URL and load last week's open findings.
3. **Compare.** Run /seo drift compare to see what changed since the baseline.
4. **Dig into changes.** Run /seo technical or /seo page on the pages that moved.
5. **Synthesize.** Walk the PERCEIVE, ANALYZE, VALIDATE and ACT phases and sort findings by priority.
6. **Refresh baseline.** After you accept the fixes, run /seo drift baseline again for next week.

Stop rule: Stops after one site and at most 10 pages analysed per run.

## Permissions

- Writes: loops/seo-drift-audit-loop/**
- Network: status.search.google.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/seo-drift-audit-loop/history.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every Monday morning. Verification: doctor, baseline and report. Memory: loops/seo-drift-audit-loop/history.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
