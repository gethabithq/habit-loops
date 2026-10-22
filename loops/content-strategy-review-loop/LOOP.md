---
name: content-strategy-sms
title: Content Strategy skill
repo: blacktwist/social-media-skills
license: MIT
url: https://gethabit.dev/skills/blacktwist/content-strategy-sms
---

# Content Strategy skill

The content strategy skill helps creators and brands decide what to post on social media: content pillars, topic clusters, content mix per platform and the gaps they can own.

- Install the skill: `npx skills add blacktwist/social-media-skills --skill content-strategy-sms`
- Source: https://github.com/blacktwist/social-media-skills/tree/HEAD/skills/content-strategy-sms
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You don't know what to post; You define content pillars; You plan your content mix.
Skip it when: You need a posting calendar; You need individual posts written.

# Make it a habit: A content strategy that stays current.

Each quarter your agent reads your social media context and the last strategy, asks only the missing discovery questions, rebuilds three to five pillars, topic clusters, weekly mix and gaps to own, and asks you to confirm before saving. The strategy file is the memory.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** quarterly strategy review (schedule; Claude Code routine; `0 9 1 1,4,7,10 *`)
- **Verification:** you confirm the strategy. Hard checks: strategy has 3 to 5 pillars; promotional content stays at 15% or less; each pillar has a topic cluster with cornerstone and supporting topics; the document lists 3 to 5 content gaps. On fail: retry, max 1 retries.
- **Memory:** content strategy document at `loops/content-strategy-review-loop/strategy.md`. Read first: the current strategy and last quarter's notes.

## Steps

1. **Read context.** Read .agents/social-media-context-sms.md and the current strategy.
2. **Ask gaps only.** Ask grouped questions on goals, performance, peers and time that the files do not answer.
3. **Build pillars.** Define 3 to 5 pillars with angle, credibility, subtopics and formats.
4. **Map clusters.** Classify topics as cornerstone or supporting per pillar.
5. **Set mix and edge.** Set the weekly mix per platform and name gaps and underserved segments.
6. **You confirm.** Show the document, apply your edits and save it.

Stop rule: Stops after one strategy document per run.

## Permissions

- Writes: loops/content-strategy-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/content-strategy-review-loop/strategy.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: quarterly strategy review. Verification: you confirm the strategy. Memory: loops/content-strategy-review-loop/strategy.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
