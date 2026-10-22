---
name: amazon-product-research
title: Amazon Product Research skill
repo: nexscope-ai/Amazon-Skills
license: MIT
url: https://gethabit.dev/skills/nexscope-ai/amazon-product-research
---

# Amazon Product Research skill

The amazon product research skill helps Amazon sellers check a product idea: demand, competition, profit potential, entry barriers and risk, rolled into one score from 1 to 10 with a clear recommendation.

- Install the skill: `npx skills add nexscope-ai/Amazon-Skills --skill amazon-product-research`
- Source: https://github.com/nexscope-ai/Amazon-Skills/tree/HEAD/amazon-product-research
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You test a new product idea; You compare two products to sell; You research a niche on Amazon Germany or another marketplace.
Skip it when: You need live sales data; You do not sell on Amazon.

# Make it a habit: Fresh scores for watched products.

Every week your agent re-researches the products on your watch list with web_search and web_fetch: demand, competition, profit potential and entry barriers. It scores each one from 1 to 10, compares with last week and keeps the scores in a board.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every Monday (schedule; Claude Code routine; `0 8 * * 1`)
- **Verification:** all factors scored. Hard checks: each product has a 1-10 score for all 8 factors; overall score uses the stated factor weights; report has every section of the output format. On fail: retry, max 1 retries.
- **Memory:** product score board at `loops/amazon-product-watch-loop/board.md`. Read first: watch list and last week's scores per product.

## Steps

1. **Read the board.** Your agent reads the watch list and the previous scores.
2. **Market data.** It uses web_search for demand, category and seasonal signals.
3. **Competition.** It checks competitor count, brand dominance and review spread.
4. **Validate demand.** It uses web_fetch on Google Trends and looks at reddit threads.
5. **Profit and entry.** It rates profit potential, regulation and sourcing barriers.
6. **Score and compare.** It weights the 8 factors into one score and marks changes since last week.

Stop rule: Stops after 5 products per run.

## Permissions

- Writes: loops/amazon-product-watch-loop/**
- Network: trends.google.com, amazon.com, reddit.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/amazon-product-watch-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every Monday. Verification: all factors scored. Memory: loops/amazon-product-watch-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
