---
name: gws-calendar
title: gws calendar skill
repo: googleworkspace/cli
license: Apache-2.0
url: https://gethabit.dev/skills/googleworkspace/gws-calendar
---

# gws calendar skill

The gws calendar skill lets your agent manage Google Calendar through the gws CLI: list and create events, read the agenda across calendars, check free and busy times and manage calendar lists. For people who want their agent to handle scheduling.

- Install the skill: `npx skills add googleworkspace/cli --skill gws-calendar`
- Source: https://github.com/googleworkspace/cli/tree/HEAD/skills/gws-calendar
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You want your upcoming agenda; You need to create or update events; You check free and busy times.
Skip it when: You do not use Google Calendar; You have no gws CLI set up.

# Make it a habit: Start each day with your agenda.

Every weekday morning your agent runs gws calendar +agenda to list upcoming events across all calendars and writes a short agenda note. It only reads, never changes events, and keeps yesterday's note to spot new or moved events.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekday morning agenda (schedule; Claude Code routine or cron; `30 7 * * 1-5`)
- **Verification:** agenda read succeeds. Hard checks: gws calendar +agenda exits without an error; the agenda note file exists for today; the note holds no tokens or keys; no write method such as insert, patch or delete was called. On fail: notify, max 1 retries.
- **Memory:** daily agenda notes at `loops/calendar-agenda-loop/agenda.md`. Read first: yesterday's agenda, to flag new or moved events.

## Steps

1. **Read shared rules.** Read ../gws-shared/SKILL.md for sign-in, flags and safety rules first.
2. **Inspect if needed.** Use gws calendar --help or gws schema calendar.<resource>.<method> before any other call.
3. **Get the agenda.** Run gws calendar +agenda to list upcoming events across all calendars.
4. **Compare.** Mark events that are new or changed since yesterday's note.
5. **Write the note.** Save today's agenda as a short list with times and titles.

Stop rule: Stops after one agenda read per run and one retry; it never writes to the calendar.

## Permissions

- Writes: loops/calendar-agenda-loop/**
- Network: googleapis.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/calendar-agenda-loop/agenda.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekday morning agenda. Verification: agenda read succeeds. Memory: loops/calendar-agenda-loop/agenda.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
