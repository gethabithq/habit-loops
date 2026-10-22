---
name: session-history
title: Session History skill
repo: rohitg00/agentmemory
license: Apache-2.0
url: https://gethabit.dev/skills/rohitg00/session-history
---

# Session History skill

The session history skill shows recent agent sessions on a project as a clean timeline, using agentmemory. It is for developers who want to know what earlier sessions did, without invented entries.

- Install the skill: `npx skills add rohitg00/agentmemory --skill session-history`
- Source: https://github.com/rohitg00/agentmemory/tree/HEAD/plugin/skills/session-history
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You ask what was done last time; You want an overview of past sessions; You return to a project after a break.
Skip it when: You need a search by topic; agentmemory is not installed.

# Make it a habit: See past sessions every week.

Each Monday morning your agent calls memory_sessions for this project and writes a timeline of the last 20 sessions with status, highlights and observation counts. A check makes sure every line came from the tool. The timeline is kept in the loop folder.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every Monday morning (schedule; Claude Code routine; `0 8 * * 1`)
- **Verification:** timeline matches tool output. Hard checks: every session shown is in the memory_sessions response; observation count per session matches the response; sessions are in reverse chronological order; only sessions of the current project are listed. On fail: retry, max 1 retries.
- **Memory:** weekly session timelines at `loops/session-history-loop/log.md`. Read first: the newest session id from last week's timeline.

## Steps

1. **Find the project.** Your agent takes the exact project id from the host, or pages with nextCursor and matches the cwd.
2. **Fetch sessions.** It calls memory_sessions with a limit of 20 and keeps the scope filters on every page.
3. **Build the timeline.** Newest first, each line shows the short session id, project, start time and status.
4. **Add highlights.** For sessions with observations it adds type and title, the count, and summary decisions when they exist.
5. **Check the list.** Nothing is invented or merged, and a partial page is marked as partial.
6. **Save the log.** The timeline is added to the run log for next week.

Stop rule: Stops after 20 sessions or when nextCursor is null, with one retry.

## Permissions

- Writes: loops/session-history-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/session-history-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every Monday morning. Verification: timeline matches tool output. Memory: loops/session-history-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
