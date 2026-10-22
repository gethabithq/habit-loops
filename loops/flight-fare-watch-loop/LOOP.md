---
name: google-flights
title: Google Flights skill
repo: skillhq/flight-search
license: MIT
url: https://gethabit.dev/skills/skillhq/google-flights
---

# Google Flights skill

The google flights skill lets an agent search Google Flights with agent-browser, read flight times and fares, compare economy and business, and pull booking links. For travellers who want flight options without clicking through the site.

- Install the skill: `npx skills add skillhq/flight-search --skill google-flights`
- Source: https://github.com/skillhq/flight-search
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You compare flights between two cities; You want nonstop options for set dates; You need booking links for one flight.
Skip it when: You want to complete a purchase; You need hotels or rental cars.

# Make it a habit: See fare changes on your route.

Each morning your agent opens a Google Flights search URL for one saved route with agent-browser, reads the results snapshot and lists the flights in compact form. A fare log keeps each day's results so the next run shows what changed.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every morning at seven (schedule; Claude Code routine or cron; `0 7 * * *`)
- **Verification:** flights found in snapshot. Hard checks: the snapshot holds at least one flight link; the travel date is in the future; no CAPTCHA or consent page left open. On fail: notify, max 1 retries.
- **Memory:** daily fare log at `loops/flight-fare-watch-loop/fares.md`. Read first: the saved route and yesterday's results.

## Steps

1. **Read the route.** Your agent loads origin, destination and dates from the fare log.
2. **Open the search.** It opens the ?q= search URL with agent-browser and waits with --load networkidle.
3. **Snapshot results.** It takes a snapshot with snapshot -i and reads each flight link.
4. **Compare cabins.** For an international route it also runs a business session and matches flights by airline and time.
5. **Write the list.** It writes the flights in the compact list format and notes changes since the last run.
6. **Close sessions.** It closes the browser sessions and never starts a purchase.

Stop rule: Stops after one route and one retry per run; a CAPTCHA stops the run at once.

## Permissions

- Writes: loops/flight-fare-watch-loop/**
- Network: www.google.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/flight-fare-watch-loop/fares.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every morning at seven. Verification: flights found in snapshot. Memory: loops/flight-fare-watch-loop/fares.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
