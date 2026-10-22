---
name: programmatic-seo
title: Programmatic SEO skill
repo: coreyhaines31/marketingskills
license: MIT
url: https://gethabit.dev/skills/coreyhaines31/programmatic-seo
---

# Programmatic SEO skill

Programmatic SEO is a skill that plans and checks SEO pages built at scale from templates and data, with 12 playbooks, linking and indexation rules. For marketers and developers building many similar pages.

- Install the skill: `npx skills add coreyhaines31/marketingskills --skill programmatic-seo`
- Source: https://github.com/coreyhaines31/marketingskills/tree/HEAD/skills/programmatic-seo
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You want location, comparison or integration pages; You build many pages from one template; You need a pre-launch check for page sets.
Skip it when: You need an audit of existing SEO issues; You plan a handful of hand-written pages.

# Make it a habit: Template pages stay unique and indexable.

When the data behind your template pages changes, your agent rebuilds the page set and runs the pre-launch checklist. It lists pages that fail, and after your OK sets them to noindex and removes them from the XML sitemap. A run log keeps the counts.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** page data changed (event; GitHub Actions or Claude Code routine; `push that changes the data path named in loops/programmatic-seo-quality-loop/config.md`)
- **Verification:** checklist passes, you approve. Hard checks: every page has a unique title and meta description; no two pages share the same intro text; every page is in the XML sitemap; no orphan pages; no conflicting noindex; no two pages target the same keyword. On fail: notify, max 1 retries.
- **Memory:** page counts and failures at `loops/programmatic-seo-quality-loop/run-log.md`. Read first: page count and failed checks from the last run.

## Steps

1. **Read context.** Read .agents/product-marketing.md if it exists, plus config.md with the playbook, template, data and sitemap paths.
2. **Check the pattern.** Confirm the keyword pattern, its variables and the data that fills each page.
3. **Check uniqueness.** Make sure each page has its own value, not just swapped variables.
4. **Check linking.** Confirm the hub links every spoke and related spokes link each other.
5. **Run the checklist.** Check titles, headings, schema, sitemap, crawlability and noindex for every page.
6. **Ask before holding back.** Show you the hold list of very thin or duplicate pages and wait for your OK.
7. **Hold back and log.** Set noindex on approved pages, remove them from the XML sitemap, and log counts and failures.

Stop rule: Stops after one page set per run, with at most 1 retry.

## Permissions

- Writes: loops/programmatic-seo-quality-loop/**, the template and sitemap files named in loops/programmatic-seo-quality-loop/config.md
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/programmatic-seo-quality-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: page data changed. Verification: checklist passes, you approve. Memory: loops/programmatic-seo-quality-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
