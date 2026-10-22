---
name: gws-drive
title: Google Drive (gws) skill
repo: googleworkspace/cli
license: Apache-2.0
url: https://gethabit.dev/skills/googleworkspace/gws-drive
---

# Google Drive (gws) skill

The Google Drive (gws) skill lets your agent manage Drive files, folders, shared drives, permissions, comments and revisions through the gws command line, for teams who want their agent to work in Google Drive.

- Install the skill: `npx skills add googleworkspace/cli --skill gws-drive`
- Source: https://github.com/googleworkspace/cli/tree/HEAD/skills/gws-drive
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You track what changed in Drive; You check who a file is shared with; You upload or copy files by script.
Skip it when: You do not use Google Drive; gws is not installed.

# Make it a habit: Know what changed in Drive.

Every morning your agent asks gws drive changes list for everything new since the last saved page token, checks the sharing of changed files with permissions list and writes a short digest. It keeps the page token so no change is read twice.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every morning (schedule; Claude Code routine or cron; `0 8 * * *`)
- **Verification:** token saved, digest written. Hard checks: gws schema run for each method before the call; fields parameter set where the method requires it; new page token saved in the memory file; digest file exists with a count of changes. On fail: notify, max 1 retries.
- **Memory:** saved page token at `loops/drive-changes-digest-loop/state.md`. Read first: the page token from the last run.

## Steps

1. **Read shared rules.** Your agent reads ../gws-shared/SKILL.md for auth, global flags and security rules.
2. **Load the token.** It reads the saved page token, or gets one with changes getStartPageToken.
3. **List changes.** It runs gws drive changes list from that token, after checking gws schema.
4. **Check sharing.** For each changed file it runs permissions list to see who has access.
5. **Write the digest.** It writes what changed and who can see it.
6. **Save the token.** It stores the new page token for the next run.

Stop rule: Stops after 100 changes per run; the rest wait for the next run.

## Permissions

- Writes: loops/drive-changes-digest-loop/**
- Network: Google Drive API via gws
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/drive-changes-digest-loop/state.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every morning. Verification: token saved, digest written. Memory: loops/drive-changes-digest-loop/state.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
