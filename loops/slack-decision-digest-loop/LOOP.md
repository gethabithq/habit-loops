---
name: slack-search
title: Slack Search skill
repo: slackapi/slack-skills-plugin
license: MIT
url: https://gethabit.dev/skills/slackapi/slack-search
---

# Slack Search skill

The slack search skill finds messages, files, channels and people across Slack with the search MCP tools, using modifiers such as in:, from: and before:, file-type filters and thread follow-ups, for anyone gathering Slack context.

- Install the skill: `npx skills add slackapi/slack-skills-plugin --skill slack-search`
- Source: https://github.com/slackapi/slack-skills-plugin/tree/HEAD/skills/slack-search
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: finding a past decision in Slack; locating a shared file; gathering context before answering.
Skip it when: reading Slack platform docs; sending a message.

# Make it a habit: Weekly decisions found and summarised.

Every Friday, your agent searches public Slack channels for the week's decisions and open questions with in:, after: and keyword searches, reads each thread for context and writes a digest. Threads already covered stay in a log.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every Friday (schedule; Claude Code routine; `0 16 * * 5`)
- **Verification:** every item has thread. Hard checks: every digest item links a message found by search; each threaded hit was read with slack_read_thread; no AND, OR, NOT or parentheses in queries; only slack_search_public used unless consent was given. On fail: retry, max 1 retries.
- **Memory:** covered threads log at `loops/slack-decision-digest-loop/log.md`. Read first: threads already in earlier digests.

## Steps

1. **Search broadly.** Your agent starts with a natural language question about this week's decisions.
2. **Narrow down.** It adds in:channel-name and after:YYYY-MM-DD filters if results are too many.
3. **Split searches.** It searches the topic, then people, then specific channels.
4. **Read context.** It reads each thread with slack_read_thread and nearby messages with slack_read_channel.
5. **Write the digest.** It lists decisions and open questions with links and skips threads already covered.

Stop rule: Stops after one digest per run, with at most 20 results per search page.

## Permissions

- Writes: loops/slack-decision-digest-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/slack-decision-digest-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every Friday. Verification: every item has thread. Memory: loops/slack-decision-digest-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
