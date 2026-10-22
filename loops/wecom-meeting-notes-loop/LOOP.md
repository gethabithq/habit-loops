---
name: wecomcli-meeting
title: WeCom CLI Meeting skill
repo: WecomTeam/wecom-cli
license: MIT
url: https://gethabit.dev/skills/wecomteam/wecomcli-meeting
---

# WeCom CLI Meeting skill

The wecom cli meeting skill manages WeCom online meetings through wecom-cli: create, list, search, update, cancel, read AI notes and to-dos, and pull full transcripts, for teams on WeChat Work.

- Install the skill: `npx skills add WecomTeam/wecom-cli --skill wecomcli-meeting`
- Source: https://github.com/WecomTeam/wecom-cli/tree/HEAD/skills/wecomcli-meeting
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You want a summary of a WeCom meeting; You need the word-for-word transcript; You want to book an online meeting with colleagues.
Skip it when: The event is an offline calendar entry; The meeting repeats and you want to change it.

# Make it a habit: Every meeting gets its notes.

Each workday evening your agent lists the day's WeCom online meetings with wecom-cli, pulls the ready notes and to-dos with meeting get, falls back to the transcript when none exist, and logs which meetings are done.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** Workdays at 18:00 (schedule; Claude Code routine or cron; `0 18 * * 1-5`)
- **Verification:** notes or transcript found. Hard checks: meeting get is called with at most 10 meeting_ids per batch; has_more is false before the transcript is used; notes come from has_note_permission true or from original_data; no userid appears in the output. On fail: notify, max 2 retries.
- **Memory:** summarised meetings log at `loops/wecom-meeting-notes-loop/run-log.md`. Read first: meeting_ids already summarised.

## Steps

1. **Shared checks.** The agent first completes the wecomcli-shared skill checks.
2. **Read the reference.** It reads references/meeting-list.md before it runs any command, as the skill requires.
3. **List meetings.** It runs wecom-cli meeting list for the day and skips meetings already in the log.
4. **Get notes.** It runs meeting get and uses note_content and todo_content when has_note_permission is true.
5. **Transcript fallback.** Without notes it reads references/meeting-original-get.md and pages meeting original get until has_more is false.
6. **Report.** It shows subject, time and attendee names, says plainly when nothing exists, and asks you when a choice is unclear.

Stop rule: Stops after the day's meetings, at most 10 per meeting get call and 2 retries per failed call.

## Permissions

- Writes: loops/wecom-meeting-notes-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/wecom-meeting-notes-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: Workdays at 18:00. Verification: notes or transcript found. Memory: loops/wecom-meeting-notes-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
