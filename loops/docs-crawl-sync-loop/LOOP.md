---
name: tavily-crawl
title: Tavily Crawl skill
repo: tavily-ai/skills
license: MIT
url: https://gethabit.dev/skills/tavily-ai/tavily-crawl
---

# Tavily Crawl skill

The tavily crawl skill crawls a website through the Tavily CLI and extracts content from many pages, with depth, breadth and path filters, and can save each page as a local markdown file. For developers collecting docs.

- Install the skill: `npx skills add tavily-ai/skills --skill tavily-crawl`
- Source: https://github.com/tavily-ai/skills/tree/HEAD/skills/tavily-crawl
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: Downloading a docs section; Bulk-extracting pages from one domain; Saving a site as markdown.
Skip it when: You need a single page; You do not have a URL yet.

# Make it a habit: Fresh local copy of docs.

Every week the agent crawls one documentation section with tvly crawl, using --select-paths, --max-depth and --limit, and saves each page as markdown with --output-dir. A run log keeps the paths crawled and the page count.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every Monday early (schedule; Claude Code routine; `0 5 * * 1`)
- **Verification:** crawl output check. Hard checks: tvly crawl finishes without an authentication error; the output directory holds more than zero .md files; the page count stays at or under --limit. On fail: notify, max 1 retries.
- **Memory:** crawl log at `loops/docs-crawl-sync-loop/runs.md`. Read first: last crawl URL, path filters and page count.

## Steps

1. **Check the CLI.** If tvly is missing or not signed in, the run stops and leaves login to the user.
2. **Map first.** It uses tavily-map to see the site structure before a full crawl.
3. **Set limits.** It starts with --max-depth 1 and a --limit, and scales up only when needed.
4. **Crawl.** It runs tvly crawl with --select-paths for the docs section.
5. **Save pages.** It uses --output-dir to write each page as a markdown file.
6. **Log.** It records the page count and compares it with the last run.

Stop rule: Stops after one site and at most 50 pages per run.

## Permissions

- Writes: ./docs/**, loops/docs-crawl-sync-loop/**
- Network: docs.example.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/docs-crawl-sync-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every Monday early. Verification: crawl output check. Memory: loops/docs-crawl-sync-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
