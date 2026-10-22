---
name: landing-page-conversion-audit
title: Landing Page Conversion Audit skill
repo: autonnel/autonnel-skills
license: Apache-2.0
url: https://gethabit.dev/skills/autonnel/landing-page-conversion-audit
---

# Landing Page Conversion Audit skill

The landing page conversion audit skill reviews a landing, sales or checkout page for conversion leaks and returns a short fix list ranked by expected impact. For marketers whose paid traffic does not convert.

- Install the skill: `npx skills add autonnel/autonnel-skills --skill landing-page-conversion-audit`
- Source: https://github.com/autonnel/autonnel-skills/tree/HEAD/landing-page-conversion-audit
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: Paid traffic does not convert; You want a CRO review; Checkout drop-off is high.
Skip it when: The page has no traffic yet; The offer or audience is the problem.

# Make it a habit: Conversion leaks ranked every month.

Once a month your agent audits your landing page against ad message match, mobile fold, offer, form, trust, post-purchase path and measurement, and writes a ranked fix list. A hard check enforces the report shape. A board keeps open fixes for the next audit.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** monthly page audit (schedule; Claude Code routine; `0 7 1 * *`)
- **Verification:** report shape enforced. Hard checks: report has Verdict, Fix now, Test don't guess, Not a problem and Could not check sections; Fix now list has 7 items or fewer; no fix claims a percentage lift; every missing input is listed under Could not check. On fail: retry, max 1 retries.
- **Memory:** open conversion fixes at `loops/landing-page-audit-loop/board.md`. Read first: fixes still open and items marked not a problem last time.

## Steps

1. **Gather inputs.** Fetch the rendered page and collect traffic source, sessions, conversions, drop-off and device split, noting what is missing.
2. **Run the checks.** Work through message match, mobile fold, offer clarity, form friction, trust, the path after the button and measurement in that order.
3. **Check the data size.** If sessions or conversions are too few, say the data cannot separate signal from noise and rank by friction.
4. **Rank and report.** Write the fixed report shape with element, failure mode, change, effort and confidence per fix.
5. **Route bigger fixes.** Point dead-end thank-you pages to post-purchase-upsell-flow and missing click ids to server-side-conversion-tracking.
6. **Update the board.** Add new fixes and close the ones the page now passes.

Stop rule: One page per run, at most 7 fixes, one retry if the report shape fails.

## Permissions

- Writes: loops/landing-page-audit-loop/**
- Network: your landing page
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/landing-page-audit-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: monthly page audit. Verification: report shape enforced. Memory: loops/landing-page-audit-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
