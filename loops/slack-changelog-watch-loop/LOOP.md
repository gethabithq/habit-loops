---
name: slack-docs
title: Slack Docs skill
repo: slackapi/slack-skills-plugin
license: MIT
url: https://gethabit.dev/skills/slackapi/slack-docs
---

# Slack Docs skill

The slack docs skill finds and reads official Slack platform documentation at docs.slack.dev as clean markdown, using the docs search API, per-page markdown and index files, for developers building on Slack.

- Install the skill: `npx skills add slackapi/slack-skills-plugin --skill slack-docs`
- Source: https://github.com/slackapi/slack-skills-plugin/tree/HEAD/skills/slack-docs
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: a how-to question about Slack features; looking up an API method or scope; summarising a pasted docs.slack.dev link.
Skip it when: searching messages in a workspace; writing a Slack message.

# Make it a habit: Slack platform changes never surprise you.

Every week, your agent searches the docs.slack.dev changelog category, fetches new pages as markdown and summarises what affects your Slack app, citing each Source URL. Pages already read are kept in a log so only new changes are reported.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every Monday (schedule; Claude Code routine; `0 9 * * 1`)
- **Verification:** every claim cites source. Hard checks: every summary item cites a fetched Source URL; no URL is used that the search API or sitemap did not return; search request includes a category. On fail: retry, max 1 retries.
- **Memory:** read changelog pages at `loops/slack-changelog-watch-loop/log.md`. Read first: changelog URLs already summarised.

## Steps

1. **Search the changelog.** Your agent calls the docs search API with category changelog.
2. **Skip known pages.** It drops URLs already in the log.
3. **Fetch as markdown.** It appends .md to each new page and fetches it, keeping the Source line.
4. **Fall back.** If search fails, it scans llms-sitemap.md instead of guessing URLs.
5. **Summarise impact.** It writes what changed and which tool, such as Bolt or the Slack CLI, is affected.

Stop rule: Stops after one weekly summary, with at most 10 new pages fetched.

## Permissions

- Writes: loops/slack-changelog-watch-loop/**
- Network: docs.slack.dev
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/slack-changelog-watch-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every Monday. Verification: every claim cites source. Memory: loops/slack-changelog-watch-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
