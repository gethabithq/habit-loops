---
name: serenity-skill
title: Serenity.skill skill
repo: muxuuu/serenity-skill
license: MIT
url: https://gethabit.dev/skills/muxuuu/serenity-skill
---

# Serenity.skill skill

The serenity.skill skill helps ordinary investors research technology and advanced-manufacturing companies through supply-chain bottleneck analysis, with dated evidence and conditions that change the judgment.

- Install the skill: `npx skills add muxuuu/serenity-skill --skill serenity-skill`
- Source: https://github.com/muxuuu/serenity-skill
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You scan a technology theme; You challenge a company's supplier claim; You compare research candidates.
Skip it when: You want trade signals; You need personal financial advice.

# Make it a habit: Dated research priorities, rechecked monthly.

Each month your agent rescans a technology theme with supply-chain bottleneck analysis, checks current filings for each candidate, and ranks research priority with dated evidence and a condition that would change it. A memo file keeps last month's judgments.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** monthly theme rescan (schedule; Claude Code routine; `0 8 1 * *`)
- **Verification:** every claim dated. Hard checks: each candidate has a dated source and reporting period; each candidate has a condition that would change its priority; shortlist holds 5 candidates or fewer. On fail: retry, max 1 retries.
- **Memory:** research memo at `loops/supply-chain-research-loop/memo.md`. Read first: last month's priorities and the conditions to watch.

## Steps

1. **Frame the change.** Name the demand or technical change and the constraint that matters.
2. **Map the chain.** Compare supply-chain layers and the alternatives customers can use.
3. **Check exposure.** Test what each company sells and its commercial stage against current disclosures.
4. **Check earnings.** Judge whether demand can turn into revenue, margins and cash flow.
5. **Counterargument.** State what evidence would make the priority fall.
6. **Rank and compare.** Give high, medium or low research priority and note changes since last month.

Stop rule: Stops after one theme and at most 5 candidates per run.

## Permissions

- Writes: loops/supply-chain-research-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/supply-chain-research-loop/memo.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: monthly theme rescan. Verification: every claim dated. Memory: loops/supply-chain-research-loop/memo.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
