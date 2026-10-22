---
name: content-strategy
title: Content Strategy skill
repo: coreyhaines31/marketingskills
license: MIT
url: https://gethabit.dev/skills/coreyhaines31/content-strategy
---

# Content Strategy skill

Content strategy is a skill that plans what content to create: pillars, topic clusters, scored priorities and a balanced calendar, from customer research and search data. For marketers and founders.

- Install the skill: `npx skills add coreyhaines31/marketingskills --skill content-strategy`
- Source: https://github.com/coreyhaines31/marketingskills/tree/HEAD/skills/content-strategy
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You do not know what to write about; You want content pillars and clusters; You want ranked topics for a calendar.
Skip it when: You need a single piece written; You need a technical SEO audit.

# Make it a habit: A ranked content plan each month.

Each month your agent reads the product context, mines forums and competitor blogs for ideas, scores every idea on the four weighted factors and updates the plan. Hard checks confirm the weighted totals, the data behind each search score and an information-gain line. The board keeps ranked topics.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** first of the month (schedule; Claude Code routine; `0 8 1 * *`)
- **Verification:** scores backed, gain line. Hard checks: the plan has 3 to 5 pillars; every total equals the 40/30/20/10 weighted sum of its four scores; every Search Potential score cites a keyword export or is marked estimate; every searchable topic has an information-gain sentence that names the top results read; every topic is marked searchable, shareable or both. On fail: retry, max 1 retries.
- **Memory:** ranked topic board at `loops/content-strategy-loop/board.md`. Read first: ranked topics, what shipped and what is still open.

## Steps

1. **Read context.** Read .agents/product-marketing.md if it exists and ask you only for missing context.
2. **Gather ideas.** Search site:reddit.com, site:quora.com and site:competitor.com/blog, plus any keyword exports or transcripts you give.
3. **Gate searchable ideas.** Read the top results and write one sentence on what the piece adds, or drop it.
4. **Score.** Score each idea 1 to 10 per factor. Take Search Potential from your Ahrefs, SEMrush or GSC export, else mark it estimate.
5. **Balance.** Split the calendar roughly 60/30/10 across searchable, shareable and experimental.
6. **Update the board.** Write pillars, priority topics and the cluster map into the board.

Stop rule: Stops after one plan per month with at most 20 scored ideas.

## Permissions

- Writes: loops/content-strategy-loop/**
- Network: reddit.com, quora.com, the competitor domains you name (site:competitor.com/blog)
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/content-strategy-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: first of the month. Verification: scores backed, gain line. Memory: loops/content-strategy-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
