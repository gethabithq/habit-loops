---
name: qqmusic
title: QQ Music skill
repo: tencentmusic/qqmusic-skills
license: Apache-2.0
url: https://gethabit.dev/skills/tencentmusic/qqmusic
---

# QQ Music skill

Qq music is a skill for QQ Music listeners who want to search songs, albums and artists, get daily picks, charts and AI playlists, and read listening reports through the QQ Music agent gateway.

- Install the skill: `npx skills add tencentmusic/qqmusic-skills --skill qqmusic`
- Source: https://github.com/tencentmusic/qqmusic-skills/tree/HEAD/qqmusic
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You want today's song picks; You want a weekly listening report; You search a song or artist.
Skip it when: You use another music service; You want bulk catalog data.

# Make it a habit: Weekly listening report, plus version check.

Every week, your agent fetches your QQ Music listening report and daily picks through the gateway, lists them with play links, and checks whether a new skill version exists for you to decide on. It keeps past reports to compare.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly on Sunday (schedule; Claude Code routine; `0 19 * * 0`)
- **Verification:** gateway returns no error. Hard checks: ret and sub_ret are empty or 0; every request carries comm.skill_version; no real key appears in any curl command. On fail: notify, max 1 retries.
- **Memory:** weekly listening reports at `loops/qqmusic-weekly-report-loop/run-log.md`. Read first: last week's report and the skill version seen.

## Steps

1. **Check the key.** Check $QQMUSIC_API_KEY and ask the user for it if it is not set.
2. **Read the docs.** Read me.md and discover.md before calling their endpoints.
3. **Get the report.** Call /me/report for the week with params and comm.skill_version.
4. **Get daily picks.** Call /discover/daily-mix and list songs with name, artist and play link.
5. **Check version.** Follow version.md to check for a new skill version and let the user decide.
6. **Log the week.** Write the report summary into the run log to compare next week.

Stop rule: Stops after three gateway calls per run, with one retry.

## Permissions

- Writes: loops/qqmusic-weekly-report-loop/**, ~/.bashrc, ~/.zshrc
- Network: a.y.qq.com, i2.y.qq.com
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/qqmusic-weekly-report-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly on Sunday. Verification: gateway returns no error. Memory: loops/qqmusic-weekly-report-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
