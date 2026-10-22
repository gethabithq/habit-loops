---
name: flyai
title: FlyAI skill
repo: alibaba-flyai/flyai-skill
license: MIT
url: https://gethabit.dev/skills/alibaba-flyai/flyai
---

# FlyAI skill

The flyai skill lets an agent search flights, hotels, trains, attractions and events with the flyai-cli, which calls Fliggy MCP services and returns JSON with booking links. For travellers planning trips with an agent.

- Install the skill: `npx skills add alibaba-flyai/flyai-skill --skill flyai`
- Source: https://github.com/alibaba-flyai/flyai-skill/tree/HEAD/skills/flyai
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You compare flights and hotels; You plan a multi-day trip; You look for attraction tickets.
Skip it when: You want the agent to pay for you; You need car or hotel loyalty logins.

# Make it a habit: Track flight and hotel options daily.

Each morning your agent runs flyai search-flight and search-hotel for one saved trip, checks that the JSON output holds results, and writes them with images and booking links. A trip log keeps each day's options so changes stand out.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every morning at seven (schedule; Claude Code routine or cron; `0 7 * * *`)
- **Verification:** search returns valid JSON. Hard checks: each flyai command prints valid single-line JSON; at least one result is returned per search; every result with jumpUrl or detailUrl shows a booking link. On fail: notify, max 1 retries.
- **Memory:** daily trip log at `loops/flyai-trip-watch-loop/trip.md`. Read first: the saved trip and yesterday's options.

## Steps

1. **Read the trip.** Your agent loads route, dates and city from the trip log.
2. **Check the schema.** It reads references/search-flight.md and references/search-hotel.md for the exact parameters.
3. **Search flights.** It runs flyai search-flight for the saved route.
4. **Search hotels.** It runs flyai search-hotel for the destination.
5. **Write the summary.** It writes a Markdown comparison table with image lines and booking links.
6. **Log changes.** It notes what changed since the last run in the trip log.

Stop rule: Stops after one trip and two searches per run; it never books.

## Permissions

- Writes: loops/flyai-trip-watch-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/flyai-trip-watch-loop/trip.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every morning at seven. Verification: search returns valid JSON. Memory: loops/flyai-trip-watch-loop/trip.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
