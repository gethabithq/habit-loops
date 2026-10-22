---
name: seo-audit
title: SEO Audit skill
repo: coreyhaines31/marketingskills
license: MIT
url: https://gethabit.dev/skills/coreyhaines31/seo-audit
---

# SEO Audit skill

The seo audit skill has your agent check crawlability, indexation, speed, on-page SEO, content quality and international setup, then write a ranked fix plan. For site owners and marketers losing rankings or traffic.

- Install the skill: `npx skills add coreyhaines31/marketingskills --skill seo-audit`
- Source: https://github.com/coreyhaines31/marketingskills/tree/HEAD/skills/seo-audit
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: your traffic dropped; pages are not indexed; you want a regular SEO health check.
Skip it when: you want to build pages at scale; you only need to add structured data.

# Make it a habit: SEO issues found and ranked.

Each month your agent audits your site in a fixed order: crawlability, technical foundations, on-page, content quality, then authority. It writes each issue with impact, evidence, fix and priority, and the run log marks every earlier finding as fixed, open or back.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** first of the month (schedule; Claude Code routine or cron; `0 8 1 * *`)
- **Verification:** checks pass, you confirm. Hard checks: robots.txt, the XML sitemap and canonicals were checked; no 'no schema found' finding rests on web_fetch or curl alone; Core Web Vitals are compared to LCP 2.5s, INP 200ms and CLS 0.1; every finding has issue, impact, evidence, fix and priority; every finding from the last run is marked fixed, open or back. On fail: retry, max 1 retries.
- **Memory:** dated findings log at `loops/seo-audit-loop/run-log.md`. Read first: last run's findings and the status of each one.

## Steps

1. **Read the context.** Read .agents/product-marketing.md if it exists and the run log, then ask you only what is missing.
2. **Set the scope.** Agree on full site or some pages, the priority keywords and your Search Console access.
3. **Audit in order.** Check crawlability and indexation first, then speed and Core Web Vitals, then on-page, content and links.
4. **Check schema right.** Use a browser tool, the Rich Results Test or a Screaming Frog export for schema, never web_fetch alone.
5. **Check locales.** On multilingual sites, check hreflang, locale canonicals and international sitemaps.
6. **Write report and log.** Write the summary, findings and prioritized action plan to report.md, then add each finding with its status to the run log.

Stop rule: Stops after one site audit per run, with the top five issues in the summary and at most 1 retry.

## Permissions

- Writes: loops/seo-audit-loop/**
- Network: the audited domain (site:domain.com), search.google.com (Rich Results Test, and Search Console with your access)
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/seo-audit-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: first of the month. Verification: checks pass, you confirm. Memory: loops/seo-audit-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
