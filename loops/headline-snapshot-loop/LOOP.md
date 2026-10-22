---
name: the-news
title: The News skill
repo: SFKislev/The-News
license: MIT
url: https://gethabit.dev/skills/sfkislev/the-news
---

# The News skill

With the news skill, agents read live and archived front-page headlines from 20 countries through a public API, for breaking news, current events and comparing how different outlets frame a story.

- Install the skill: `npx skills add SFKislev/The-News --skill the-news`
- Source: https://github.com/SFKislev/The-News
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: Checking what is happening now in a country; Looking at headlines from a past moment; Comparing framing across outlets.
Skip it when: You need full article text; You need verified facts, not headlines.

# Make it a habit: A daily front-page brief per country.

Every morning the agent calls the country-view endpoint for each chosen country, reads the raw headlines next to the AI overviews and writes a short brief on the main stories and framing. A run log keeps timestamps and countries.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every morning (schedule; Claude Code routine; `0 7 * * *`)
- **Verification:** response check. Hard checks: each response holds a headlines array with more than zero entries; every at value is a UTC timestamp; daily-overviews ranges are 7 days or shorter. On fail: retry, max 1 retries.
- **Memory:** daily headline log at `loops/headline-snapshot-loop/runs.md`. Read first: yesterday's countries, timestamp and main stories.

## Steps

1. **Pick countries.** The agent reads the country keys to cover from the run log.
2. **Fetch snapshots.** It calls the country-view endpoint once per country.
3. **Read overviews.** It compares the current, previous and yesterday overviews.
4. **Headlines first.** Raw headlines count as the source of truth; overviews are only context.
5. **Write the brief.** It names the dominant stories and how framing differs across sources.
6. **Log.** It saves the timestamp and countries for the next run.

Stop rule: Stops after at most 5 countries per run.

## Permissions

- Writes: loops/headline-snapshot-loop/**
- Network: www.thehear.org
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/headline-snapshot-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every morning. Verification: response check. Memory: loops/headline-snapshot-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
