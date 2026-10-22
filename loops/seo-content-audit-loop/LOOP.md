---
name: seo-content
title: SEO Content skill
repo: agricidaniel/claude-seo
license: MIT
url: https://gethabit.dev/skills/agricidaniel/seo-content
---

# SEO Content skill

Seo content scores page content for E-E-A-T, usefulness, readability, thin content and AI citation readiness, and cleans up drafts by removing invisible watermark characters and stock AI phrasing. For site owners and SEO writers.

- Install the skill: `npx skills add agricidaniel/claude-seo --skill seo-content`
- Source: https://github.com/agricidaniel/claude-seo/tree/HEAD/skills/seo-content
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You audit page content quality; You check E-E-A-T signals; You clean up an AI-assisted draft.
Skip it when: You need a technical SEO audit; You want to strip provenance from content you do not own.

# Make it a habit: Weekly content quality scores.

Each week your agent audits a few key pages with seo-content: the Who, How and Why test, E-E-A-T scores, word count, readability, structure and AI citation readiness. It writes a score report per page and keeps a log to track change.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every Monday morning (schedule; Claude Code routine or cron; `0 8 * * 1`)
- **Verification:** report complete, scored. Hard checks: each report has a Content Quality Score and an AI Citation Readiness score; the E-E-A-T table lists all four factors; unreachable or gated pages are reported, not guessed. Critic: claude-opus-5-5, pass at 17/20. On fail: retry, max 1 retries.
- **Memory:** page score log at `loops/seo-content-audit-loop/scores.md`. Read first: last scores per page and open recommendations.

## Steps

1. **Pick pages.** Take the next pages from the list in the score log.
2. **Who, How, Why.** Check author, creation process and purpose for each page.
3. **Score E-E-A-T.** Rate experience, expertise, authority and trust with the skill's scoring guide.
4. **Check content metrics.** Review word count against page type, readability, headings, links and freshness.
5. **AI citation check.** Rate how quotable and well structured the page is for AI search.
6. **Check updates.** For traffic drops, run seo_updates.py --since to list Google updates in that window.
7. **Write and log.** Save the report with issues and recommendations, and add scores to the log.

Stop rule: Stops after five pages per run and one retry per report.

## Permissions

- Writes: loops/seo-content-audit-loop/**
- Network: developers.google.com, status.search.google.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/seo-content-audit-loop/scores.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every Monday morning. Verification: report complete, scored. Memory: loops/seo-content-audit-loop/scores.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
