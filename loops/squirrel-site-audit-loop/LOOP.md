---
name: audit-website
title: Audit Website (squirrelscan) skill
repo: squirrelscan/skills
license: MIT
url: https://gethabit.dev/skills/squirrelscan/audit-website
---

# Audit Website (squirrelscan) skill

Audit Website (squirrelscan) runs the squirrel CLI over a site for SEO, performance, security, accessibility and more, then maps findings to source files and fixes them until the score target is met.

- Install the skill: `npx skills add squirrelscan/skills --skill audit-website`
- Source: https://github.com/squirrelscan/skills/tree/HEAD/skills/audit-website
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You want a full site health check; You fix SEO and accessibility issues in code; You need to catch regressions after a deploy.
Skip it when: The squirrel CLI is not installed; You only need one page checked by hand.

# Make it a habit: Site score climbs every week.

Every week, or when a squirrelscan cloud audit finishes, your agent runs squirrel audit with --format llm, maps findings to source files, fixes approved batches and re-audits. It compares against the baseline with squirrel report --diff and keeps the audit ids.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly or audit event (schedule; Claude Code routine or cron; `0 6 * * 1, or squirrelscan channel event`)
- **Verification:** re-audit, build, your OK. Hard checks: project builds and existing checks pass after each batch; re-audit score reaches the target for the starting grade; count of error-level findings is zero; squirrel report --diff against the baseline shows no regression. On fail: retry, max 2 retries.
- **Memory:** audit ids and scores at `loops/squirrel-site-audit-loop/log.md`. Read first: baseline audit id, last score and findings left for human review.

## Steps

1. **Audit the site.** Your agent runs squirrel audit with --format llm, starting with --level quick.
2. **Present the report.** It shows the score, grade and top issues by severity.
3. **Confirm fixes.** It lists the fixes it can make and asks you before changing anything.
4. **Map and fix.** It finds the template, component or content file behind each finding and fixes errors first.
5. **Build check.** After each batch the project must still build and pass its checks.
6. **Re-audit.** It re-audits with --refresh and shows before and after scores.
7. **Diff and sign off.** It runs squirrel report --diff on the baseline and signs off on a --level full crawl.

Stop rule: Stops when the score target is met, only judgment calls remain, or after 2 fix batches.

## Permissions

- Writes: src/**, content/**, loops/squirrel-site-audit-loop/**
- Network: the audited site, docs.squirrelscan.com
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/squirrel-site-audit-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly or audit event. Verification: re-audit, build, your OK. Memory: loops/squirrel-site-audit-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
