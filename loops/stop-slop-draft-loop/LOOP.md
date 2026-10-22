---
name: stop-slop
title: Stop Slop skill
repo: hardikpandya/stop-slop
license: MIT
url: https://gethabit.dev/skills/hardikpandya/stop-slop
---

# Stop Slop skill

The stop slop skill helps your agent remove predictable AI writing patterns from prose: filler, formulaic structures, passive voice and em dashes, with a five part score. For writers and teams who edit drafts with AI.

- Install the skill: `npx skills add hardikpandya/stop-slop --skill stop-slop`
- Source: https://github.com/hardikpandya/stop-slop
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You edit a blog post or essay; You review AI written copy; You want a score before publishing.
Skip it when: Code or data files; Legal text with fixed wording.

# Make it a habit: Drafts ship without AI tells.

When a new draft lands, your agent runs the stop slop quick checks, scores the text on five dimensions and revises until it reaches 35 of 50. It logs the score and the patterns it cut, so the next run knows your usual tells.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** new draft committed (event; GitHub Actions or Claude Code routine; `push to drafts/**`)
- **Verification:** score 35 of 50. Hard checks: no em dash left in the draft; no 'not X, it's Y' contrast left; score is at least 35/50. Critic: claude-opus-5-5, pass at 35/50. On fail: retry, max 2 retries.
- **Memory:** scores and cut patterns at `loops/stop-slop-draft-loop/run-log.md`. Read first: patterns that came up most in past drafts.

## Steps

1. **Pick up the draft.** A new or changed draft starts the run.
2. **Cut filler.** Your agent removes filler phrases and adverbs using the phrases reference.
3. **Break structures.** It rewrites formulaic structures listed in the structures reference.
4. **Run quick checks.** It goes through the quick check list, from passive voice to em dashes.
5. **Score.** It rates directness, rhythm, trust, authenticity and density from 1 to 10.
6. **Revise or pass.** Below 35 of 50 it revises again, otherwise it saves the draft and logs the score.

Stop rule: Stops after one draft per run and at most 2 revision rounds.

## Permissions

- Writes: drafts/**, loops/stop-slop-draft-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/stop-slop-draft-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: new draft committed. Verification: score 35 of 50. Memory: loops/stop-slop-draft-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
