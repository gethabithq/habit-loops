---
name: seo-loop
title: SEO loop
outcome: Rank new pages every 21 days.
source: https://github.com/marcopatzelt/seo-loop-kit
license: MIT
url: https://gethabit.dev/loops/seo-loop
---

# SEO loop: Rank new pages every 21 days.

Every 21 days the loop reads its task board, pulls search data, writes one page per finding, lets a second agent grade it, and opens a pull request. Three weeks later it checks Search Console and reopens what did not work.

## The three decisions

- **Trigger:** every 21 days (schedule; Claude Code routine or GitHub Actions; `0 6 */21 * *`)
- **Verification:** hard check + second grader. Hard checks: build passes; title ≤ 60 chars; description ≤ 155 chars; no new noindex. Critic: claude-opus-5-5, pass at 17/20. On fail: retry, max 1 retries.
- **Memory:** task board at `loops/seo-loop/board.md`. Read first: open tasks and pages due for a 21-day check.

## Steps

1. **Check the board.** Read open tasks and pages that are due for their 21-day check.
2. **Analyze.** Pull search data and see who ranks for each target term.
3. **Create tasks.** One task per finding. Skip what the board already has.
4. **Gate.** If the page exists or the task is a duplicate, stop here.
5. **Build.** Write the page into the repo with title, description and links.
6. **Critic.** A second agent with fresh context grades it. Below 17 of 20, rewrite once.
7. **Ship.** Open a pull request. A human merges.
8. **Verify after 21 days.** Read Search Console. Ranked but no clicks? The task reopens.

Stop rule: Stops after 3 tasks per run.

## Permissions

- Writes: src/content/**, loops/seo-loop/**
- Network: api.dataforseo.com, searchconsole.googleapis.com
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/seo-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every 21 days. Verification: hard check + second grader. Memory: loops/seo-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`

Setup prompt: Read https://gethabit.dev/loops/seo-loop.md and install this loop in my project. Show me the files first.
