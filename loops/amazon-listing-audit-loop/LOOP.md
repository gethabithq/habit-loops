---
name: amazon-listing-optimization
title: Amazon Listing Optimization skill
repo: nexscope-ai/amazon-skills
license: MIT
url: https://gethabit.dev/skills/nexscope-ai/amazon-listing-optimization
---

# Amazon Listing Optimization skill

Amazon listing optimization is a skill for Amazon sellers that builds keyword-optimized listings from keywords or competitor ASINs, or audits existing listings on eight dimensions and rewrites them with missing keywords.

- Install the skill: `npx skills add nexscope-ai/amazon-skills --skill amazon-listing-optimization`
- Source: https://github.com/nexscope-ai/amazon-skills/tree/HEAD/amazon-listing-optimization
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You create a new Amazon listing; You audit an existing ASIN; You compare with competitor listings.
Skip it when: You need PPC or sales data; You do not sell on Amazon.

# Make it a habit: Listings keep their keyword coverage.

Every month, your agent fetches your Amazon listing with fetch-listing.sh, compares it with competitor keywords, scores it on eight dimensions and writes an optimized title, bullets and description with a before and after keyword coverage map.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** monthly listing audit (schedule; Claude Code routine; `0 9 1 * *`)
- **Verification:** limits and coverage met. Hard checks: title is at most 200 characters; each bullet is at most 500 characters; description is at most 2000 characters; keyword coverage after is at least coverage before. On fail: retry, max 1 retries.
- **Memory:** monthly audit scores at `loops/amazon-listing-audit-loop/run-log.md`. Read first: last audit score, coverage and target keywords.

## Steps

1. **Fetch the listing.** Run scripts/fetch-listing.sh with the ASIN and marketplace.
2. **Find keywords.** Use the given keywords or extract them from up to three competitor listings.
3. **Gap analysis.** Map which keywords appear in title, bullets and description, and which are missing.
4. **Score.** Score the eight dimensions, from title to SEO coverage.
5. **Rewrite.** Write the optimized listing in the marketplace language, showing before and after.
6. **Log.** Write the score and coverage into the run log.

Stop rule: Stops after one ASIN and three competitors per run.

## Permissions

- Writes: loops/amazon-listing-audit-loop/**
- Network: amazon.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/amazon-listing-audit-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: monthly listing audit. Verification: limits and coverage met. Memory: loops/amazon-listing-audit-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
