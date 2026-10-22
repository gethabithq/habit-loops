---
name: no-ai-slop
title: No AI Slop skill
repo: petergyang/no-ai-slop
license: MIT
url: https://gethabit.dev/skills/petergyang/no-ai-slop
---

# No AI Slop skill

The no ai slop skill edits drafts into sharper, more human writing while keeping the writer's voice, or flags AI-slop patterns without rewriting, for writers and editors.

- Install the skill: `npx skills add petergyang/no-ai-slop --skill no-ai-slop`
- Source: https://github.com/petergyang/no-ai-slop/tree/HEAD/skills/no-ai-slop
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: Your draft sounds like AI; You want a light edit that keeps your voice; You need a pattern audit without a rewrite.
Skip it when: You want an AI-detection score; You want a full rewrite in a new voice.

# Make it a habit: Drafts sound like you, not AI.

When you hand over a new draft, your agent edits it with the minimum change: cuts banned words and AI patterns, keeps your voice and checks the result against eval.md. It returns the draft with a What changed note and logs the patterns it found.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** you share a draft (manual; Claude Code session; `user pastes or shares a draft to edit or audit`)
- **Verification:** eval.md checks pass. Hard checks: edited draft passes the checks in eval.md; no word from the banned list remains; What changed section is present; short copy has no em dashes. On fail: retry, max 2 retries.
- **Memory:** patterns found at `loops/draft-deslop-loop/run-log.md`. Read first: patterns found in past drafts and voice traits to keep.

## Steps

1. **Read it all.** The agent reads the full draft before changing anything.
2. **Find the voice.** It names the core point and the voice traits to keep, like cadence and humor.
3. **Pick the job.** A detect request gets a findings list with quotes and stops there.
4. **Edit minimally.** It cuts banned words, binary contrasts, puffery and recap endings, and leaves strong lines alone.
5. **Check eval.md.** It checks the edit against eval.md and fixes until it passes.
6. **Return.** It outputs the full edited draft plus a short What changed section.

Stop rule: One draft per run, at most two check-and-fix rounds.

## Permissions

- Writes: the shared draft, loops/draft-deslop-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/draft-deslop-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: you share a draft. Verification: eval.md checks pass. Memory: loops/draft-deslop-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
