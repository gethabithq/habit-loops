---
name: seo-aeo-best-practices
title: SEO AEO Best Practices skill
repo: sanity-io/agent-toolkit
license: MIT
url: https://gethabit.dev/skills/sanity-io/seo-aeo-best-practices
---

# SEO AEO Best Practices skill

The seo aeo best practices skill from Sanity gives your agent guidance on metadata, sitemaps, hreflang, JSON-LD and EEAT, for developers who want pages ready for Google and AI answer engines.

- Install the skill: `npx skills add sanity-io/agent-toolkit --skill seo-aeo-best-practices`
- Source: https://github.com/sanity-io/agent-toolkit/tree/HEAD/skills/seo-aeo-best-practices
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You add metadata or Open Graph tags; You add JSON-LD structured data; You prepare content for AI answers.
Skip it when: You need keyword or ranking data; The site is not public.

# Make it a habit: Keep pages ready for search.

Each week your agent checks changed pages against the SEO and AEO references: metadata, Open Graph, sitemap, robots.txt, hreflang and JSON-LD. It fixes gaps, checks the build and keeps a board of open findings.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly page check (schedule; Claude Code routine; `0 7 * * 1`)
- **Verification:** metadata and schema checks. Hard checks: every checked page has a title and meta description; JSON-LD blocks parse as valid JSON; sitemap and robots.txt exist; build passes. On fail: notify, max 1 retries.
- **Memory:** open SEO findings at `loops/seo-aeo-audit-loop/board.md`. Read first: open findings and pages fixed last week.

## Steps

1. **Pick the reference.** Your agent picks the one reference that fits the task, such as references/technical-seo.md.
2. **Check metadata.** It checks titles, descriptions, Open Graph tags, sitemaps, robots.txt and hreflang.
3. **Check structured data.** It compares JSON-LD with references/structured-data.md.
4. **Check content quality.** It reviews pages with references/eeat-principles.md and references/aeo-considerations.md.
5. **Fix and record.** It fixes small gaps and puts the rest on the board.

Stop rule: Stops after 10 pages per run.

## Permissions

- Writes: src/**, loops/seo-aeo-audit-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/seo-aeo-audit-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly page check. Verification: metadata and schema checks. Memory: loops/seo-aeo-audit-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
