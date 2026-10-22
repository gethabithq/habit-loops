---
name: audit-speed
title: Audit Speed skill
repo: calm-north/seojuice-skills
license: MIT
url: https://gethabit.dev/skills/calm-north/audit-speed
---

# Audit Speed skill

The audit speed skill helps site owners and SEO teams run a deep Core Web Vitals audit with root-cause trees for LCP, CLS and INP, a resource breakdown and priority fixes.

- Install the skill: `npx skills add calm-north/seojuice-skills --skill audit-speed`
- Source: https://github.com/calm-north/seojuice-skills/tree/HEAD/skills/audit-speed
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: Your page is slow; Core Web Vitals fail in Search Console; You want to know why LCP is high.
Skip it when: You need a full technical SEO audit; You have no access to page speed data.

# Make it a habit: Core Web Vitals checked every week.

Each week your agent audits key pages for LCP, CLS, INP, FCP and TTFB, walks the root-cause trees for failing metrics, breaks down page weight and writes priority fixes. A run log keeps last week's values so regressions show up.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly speed audit (schedule; Claude Code routine or cron; `0 6 * * 3`)
- **Verification:** metrics rated, fixes listed. Hard checks: each page has values for all five metrics; every Poor or Needs Improvement metric has a root cause and fix; resource breakdown table is filled. On fail: retry, max 1 retries.
- **Memory:** weekly vitals log at `loops/audit-speed-loop/run-log.md`. Read first: last week's metric values per page.

## Steps

1. **Gather context.** Confirm pages, current scores, tech stack and known constraints.
2. **Rate metrics.** Rate each metric against the Good, Needs Improvement and Poor thresholds.
3. **Find root causes.** Walk the LCP, CLS and INP trees for each failing metric.
4. **Weigh resources.** Break down HTML, CSS, JavaScript, images, fonts and third-party size.
5. **Write the audit.** List priority fixes by impact and quick wins, compared with last week.

Stop rule: Stops after 5 pages per run.

## Permissions

- Writes: loops/audit-speed-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/audit-speed-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly speed audit. Verification: metrics rated, fixes listed. Memory: loops/audit-speed-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
