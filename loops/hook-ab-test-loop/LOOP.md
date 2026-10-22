---
name: hook-writer-sms
title: Hook Writer skill
repo: blacktwist/social-media-skills
license: MIT
url: https://gethabit.dev/skills/blacktwist/hook-writer-sms
---

# Hook Writer skill

The hook writer skill helps creators write opening lines, video hooks, YouTube titles and pin titles across nine proven patterns, adapted to each platform's limits and culture.

- Install the skill: `npx skills add blacktwist/social-media-skills --skill hook-writer-sms`
- Source: https://github.com/blacktwist/social-media-skills/tree/HEAD/skills/hook-writer-sms
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: Nobody reads past your first line; You want hook variants to test; You write a YouTube title or pin title.
Skip it when: You need the full post; You need visual design.

# Make it a habit: Learn which hooks your audience likes.

Each week your agent reads your social media context and last tests, writes five to seven labeled hook variants per planned post across the nine patterns, marks a top pick, and records A/B results in a test log so patterns that win get used more.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly hook drafting (schedule; Claude Code routine; `0 9 * * 1`)
- **Verification:** variants labeled, pick marked. Hard checks: each post gets 5 to 7 hook variants; every variant names its pattern; one variant is marked as the recommended pick with a reason; X hooks stay under 280 characters. On fail: retry, max 1 retries.
- **Memory:** hook A/B test log at `loops/hook-ab-test-loop/ab-tests.md`. Read first: past tests, winners and which patterns win per topic.

## Steps

1. **Read context.** Read .agents/social-media-context-sms.md if it exists.
2. **Read test log.** Read past A/B results to favor patterns that won.
3. **Write variants.** Write 5 to 7 hooks per post from different patterns, fitted to the platform.
4. **Pick one.** Mark the recommended hook with a one-sentence reason.
5. **Log tests.** Add new A/B pairs and record saves, comments and engagement rate for finished tests.

Stop rule: Stops after 5 posts per run.

## Permissions

- Writes: loops/hook-ab-test-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/hook-ab-test-loop/ab-tests.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly hook drafting. Verification: variants labeled, pick marked. Memory: loops/hook-ab-test-loop/ab-tests.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
