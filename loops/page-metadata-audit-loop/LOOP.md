---
name: fixing-metadata
title: Fixing Metadata skill
repo: ibelick/ui-skills
license: MIT
url: https://gethabit.dev/skills/ibelick/fixing-metadata
---

# Fixing Metadata skill

The fixing metadata skill helps your agent audit and fix HTML metadata: titles, descriptions, canonical URLs, Open Graph, Twitter cards, favicons, JSON-LD and robots tags. For web developers shipping pages that must index and share correctly.

- Install the skill: `npx skills add ibelick/ui-skills --skill fixing-metadata`
- Source: https://github.com/ibelick/ui-skills/tree/HEAD/skills/fixing-metadata
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You ship new or marketing pages; Social share previews look wrong; You set up canonical URLs.
Skip it when: Apps with no public pages; Full SEO content strategy work.

# Make it a habit: Every new page ships correct metadata.

When a pull request adds or changes pages, your agent audits titles, descriptions, canonical URLs, Open Graph, Twitter cards, icons and JSON-LD by the skill's priority list. It fixes critical issues first with a metadata-only diff and logs what it changed.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR changes pages (event; GitHub Actions or Claude Code routine; `pull_request paths: pages and layouts`)
- **Verification:** no duplicates, tags agree. Hard checks: each page has exactly one title, description, canonical and robots tag; og:url matches the canonical URL; Open Graph and Twitter image URLs are absolute; JSON-LD blocks parse as valid JSON; the diff touches only metadata. On fail: retry, max 1 retries.
- **Memory:** metadata issues per page at `loops/page-metadata-audit-loop/run-log.md`. Read first: pages with open metadata issues.

## Steps

1. **Find pages.** Your agent lists the pages in the pull request with missing or wrong metadata.
2. **Fix critical first.** It removes duplicate tags and fixes canonical and indexing problems first.
3. **Align the tags.** It makes title, description, canonical and og:url agree with each other.
4. **Check social cards.** It sets Open Graph title, description and absolute image URLs and a fitting twitter:card.
5. **Check icons and data.** It checks favicon, manifest and JSON-LD that matches real page content.
6. **Verify on a real URL.** It checks social cards on a real preview URL, not localhost.
7. **Log.** It writes the fixed and open issues per page to the run log.

Stop rule: Stops after 20 pages per run and 1 retry.

## Permissions

- Writes: src/**, loops/page-metadata-audit-loop/**
- Network: the preview deployment host
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/page-metadata-audit-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR changes pages. Verification: no duplicates, tags agree. Memory: loops/page-metadata-audit-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
