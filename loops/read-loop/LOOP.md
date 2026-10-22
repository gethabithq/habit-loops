---
name: read
title: Read skill
repo: tw93/Waza
license: MIT
url: https://gethabit.dev/skills/tw93/read
---

# Read skill

The read skill fetches a URL or PDF and returns a short grounded summary or clean Markdown, with a privacy-first local fetch and optional fallbacks. For agents that read, quote or save web pages and PDFs.

- Install the skill: `npx skills add tw93/Waza --skill read`
- Source: https://github.com/tw93/Waza/tree/HEAD/plugins/waza/skills/read
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: you want a summary of a web page; you need a PDF as clean Markdown; you want to save a page with frontmatter.
Skip it when: the text is already a local file in your repo; the URL is internal or needs a login.

# Make it a habit: Fresh summaries of saved links.

Once a week your agent fetches each URL or PDF on your reading list with the read skill, checks the fetch tier line and that the page is real content, and writes a short grounded summary. The log keeps which links were read and which failed.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every Monday morning (schedule; Claude Code routine or cron; `0 7 * * 1`)
- **Verification:** fetch status and content. Hard checks: the [fetch] stderr line shows status=ok for the used tier; the fetched text is not a login, paywall or consent shell; each summary names its original URL; a saved file never overwrites an existing one. On fail: notify, max 1 retries.
- **Memory:** links read and failed at `loops/read-loop/runs.md`. Read first: links already summarized, links that failed and the tier that failed.

## Steps

1. **Load the list.** The agent reads the run log and picks the links that are new or failed last time.
2. **Route each link.** It picks the method from the routing table, such as PDF extraction or the built-in fetcher.
3. **Fetch locally.** It runs scripts/fetch.sh without --use-proxy, so the URL goes to no third-party reader.
4. **Check the tier.** It reads the [fetch] stderr line and stops on a login or paywall page.
5. **Summarize.** It writes a few bullets grounded in the page, with the source URL and useful details.
6. **Save and log.** It saves the Markdown with frontmatter, adds -1 on a name clash and records the result.

Stop rule: At most 10 links per run, one retry per failed link.

## Permissions

- Writes: loops/read-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/read-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every Monday morning. Verification: fetch status and content. Memory: loops/read-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
