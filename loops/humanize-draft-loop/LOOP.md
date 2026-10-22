---
name: humanize-writing
title: Humanize Writing skill
repo: jpeggdev/humanize-writing
license: MIT
url: https://gethabit.dev/skills/jpeggdev/humanize-writing
---

# Humanize Writing skill

The humanize writing skill helps writers remove signs of AI-generated text: inflated significance, AI vocabulary, robotic rhythm, hedging, em dash overuse and chatbot artifacts.

- Install the skill: `npx skills add jpeggdev/humanize-writing --skill humanize-writing`
- Source: https://github.com/jpeggdev/humanize-writing
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: Your text sounds like AI; You edit a draft before publishing; You review content for AI tells.
Skip it when: You write new copy from scratch; You need academic citation checks.

# Make it a habit: Drafts lose their AI tells.

Before a draft is published, your agent runs eight editing passes: structure, inflation, vocabulary, grammar, rhythm, hedging, transitions and voice, then does the read-aloud test and adds a short changes table, keeping facts and names intact.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** draft ready for edit (event; Claude Code routine; `a new draft lands in the drafts folder`)
- **Verification:** tells removed, facts kept. Hard checks: no Tier 1 word from references/ai-tells.md remains; no chatbot artifacts remain; the changes table has 8 rows or fewer; numbers and proper nouns match the original. On fail: retry, max 1 retries.
- **Memory:** edit passes log at `loops/humanize-draft-loop/run-log.md`. Read first: tells that keep coming back.

## Steps

1. **Fix structure.** Break repeated section shapes and formulaic endings.
2. **Cut inflation.** Replace significance and promotional words with specific facts.
3. **Swap vocabulary.** Remove Tier 1 words and clusters of Tier 2 words.
4. **Fix grammar and rhythm.** Fix copula avoidance and -ing phrases, vary sentence length, count em dashes.
5. **Cut hedging.** Drop filler, vague attributions and generic transitions.
6. **Add voice.** Add a little opinion and texture where it fits.
7. **Read aloud.** Run the read-aloud test and write the changes table.

Stop rule: Stops after one draft, with at most 1 extra pass.

## Permissions

- Writes: loops/humanize-draft-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/humanize-draft-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: draft ready for edit. Verification: tells removed, facts kept. Memory: loops/humanize-draft-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
