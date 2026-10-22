---
name: seo-geo
title: SEO GEO skill
repo: ReScienceLab/opc-skills
license: Apache-2.0
url: https://gethabit.dev/skills/resciencelab/seo-geo
---

# SEO GEO skill

The seo geo skill audits a website for classic search and for AI search engines like ChatGPT, Perplexity and Claude. It checks meta tags, robots.txt, sitemaps and schema, and suggests GEO content changes. For site owners and marketers.

- Install the skill: `npx skills add ReScienceLab/opc-skills --skill seo-geo`
- Source: https://github.com/ReScienceLab/opc-skills/tree/HEAD/.agents/skills/seo-geo
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You want to be cited by AI search engines; You need a quick technical SEO check; You add JSON-LD schema to pages.
Skip it when: You need paid rank tracking data; The site is not public yet.

# Make it a habit: Site stays findable by AI search.

Each week your agent audits your site with seo-geo: it runs scripts/seo_audit.py, checks meta tags, robots.txt, sitemap and JSON-LD, and makes sure AI bots may crawl. It writes the SEO/GEO report and keeps last week's status to compare.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly site audit (schedule; Claude Code routine; `0 6 * * 1`)
- **Verification:** audit checks pass. Hard checks: robots.txt does not block Googlebot, Bingbot, PerplexityBot, ChatGPT-User, ClaudeBot or GPTBot; sitemap.xml returns content; page has a title, meta description and og tags; page has at least one application/ld+json block; H1 contains the primary keyword. On fail: notify, max 0 retries.
- **Memory:** weekly SEO reports at `loops/seo-geo-audit-loop/reports.md`. Read first: last report's status lines and open recommendations.

## Steps

1. **Read last report.** The agent opens last week's report and lists the open recommendations.
2. **Run the audit.** It runs python3 scripts/seo_audit.py on the target URL for title, meta, H1, robots, sitemap and load time.
3. **Check tags and bots.** It fetches the page, robots.txt and sitemap.xml with curl and checks AI bot access.
4. **Research keywords.** It uses WebSearch to check target keywords and what competitors rank for.
5. **Apply GEO methods.** It suggests answer-first structure, citations, statistics and FAQPage schema from references/geo-research.md.
6. **Write the report.** It fills the SEO/GEO report template with status, top three actions and GEO changes.

Stop rule: Stops after one site and at most 10 pages audited per run.

## Permissions

- Writes: loops/seo-geo-audit-loop/**
- Network: the target site, search.google.com, validator.schema.org
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/seo-geo-audit-loop/reports.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly site audit. Verification: audit checks pass. Memory: loops/seo-geo-audit-loop/reports.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
