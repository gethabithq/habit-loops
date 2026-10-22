---
name: zsxq
title: Knowledge Planet (zsxq) skill
repo: unnoo/zsxq-skill
license: MIT
url: https://gethabit.dev/skills/unnoo/zsxq
---

# Knowledge Planet (zsxq) skill

The knowledge planet (zsxq) skill helps group owners and members use zsxq-cli or the MCP tool to browse, search, post, reply, tag and run daily operations on their Knowledge Planet groups.

- Install the skill: `npx skills add unnoo/zsxq-skill --skill zsxq`
- Source: https://github.com/unnoo/zsxq-skill/tree/HEAD/skills/zsxq
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You run a Knowledge Planet group; You need a daily patrol of new content; You search or summarize group topics.
Skip it when: You do not use Knowledge Planet; You want fully automatic posting.

# Make it a habit: What needs your reply, daily.

Each morning your agent runs the daily patrol scenario on your Knowledge Planet group with zsxq-cli: new topics, unanswered questions and unreplied comments, with draft replies. Nothing is posted without your confirmation. A log keeps what was handled.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** daily group patrol (schedule; Claude Code routine; `0 8 * * *`)
- **Verification:** patrol report written. Hard checks: group_id comes from group +list, not an example value; the report lists new topics, unanswered questions and unreplied comments; no write command ran during the patrol. On fail: notify, max 1 retries.
- **Memory:** patrol log at `loops/zsxq-daily-patrol-loop/run-log.md`. Read first: items flagged yesterday and whether they were handled.

## Steps

1. **Pick the channel.** Use zsxq-cli if available, else the call_zsxq_api MCP tool.
2. **Find the group.** Get the group_id with zsxq-cli group +list.
3. **Run the patrol.** Follow references/scenarios/daily-patrol.md for new content.
4. **Find open questions.** Use get_self_answer_topics with unanswered and filter to the group.
5. **Draft replies.** Draft replies for unreplied comments without posting them.
6. **Write the report.** Write the patrol report and log the items.

Stop rule: Stops after one group and 50 items per run; read-only.

## Permissions

- Writes: loops/zsxq-daily-patrol-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/zsxq-daily-patrol-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: daily group patrol. Verification: patrol report written. Memory: loops/zsxq-daily-patrol-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
