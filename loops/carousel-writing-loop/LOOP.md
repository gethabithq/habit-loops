---
name: carousel-writer-sms
title: Carousel Writer skill
repo: blacktwist/social-media-skills
license: MIT
url: https://gethabit.dev/skills/blacktwist/carousel-writer-sms
---

# Carousel Writer skill

The carousel writer skill helps creators write slide-by-slide carousel copy for LinkedIn, Instagram, Facebook, TikTok photo carousels and Pinterest Idea Pins, with covers that earn the swipe.

- Install the skill: `npx skills add blacktwist/social-media-skills --skill carousel-writer-sms`
- Source: https://github.com/blacktwist/social-media-skills/tree/HEAD/skills/carousel-writer-sms
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You need a LinkedIn carousel; You turn an idea into slides; You write an Instagram carousel.
Skip it when: You need the visual design; You want a single post or a thread.

# Make it a habit: A ready carousel draft every week.

Each week your agent reads your social media context file, picks the carousel slot from your plan, and writes slide-by-slide copy: cover, context, one point per body slide and a CTA, within the platform's slide count. A log keeps topics and formats used.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly carousel draft (schedule; Claude Code routine; `0 9 * * 2`)
- **Verification:** slide rules hold. Hard checks: .agents/social-media-context-sms.md was read; slide count is inside the platform's range; every body slide has 30 words or fewer; deck has a cover, a context slide and a CTA slide. On fail: retry, max 1 retries.
- **Memory:** carousel topics log at `loops/carousel-writing-loop/run-log.md`. Read first: topics and formats used in recent weeks.

## Steps

1. **Read context.** Read .agents/social-media-context-sms.md, or suggest the social-media-context-sms skill if it is missing.
2. **Pick the brief.** Take topic, platform, slide count and goal from the plan.
3. **Choose a format.** Pick listicle, framework, before and after, data story or mini case study.
4. **Write slides.** Write context and body slides with one point each, then the CTA, and the cover last.
5. **Platform pass.** Apply the platform's slide ratio, text density and caption notes.

Stop rule: Stops after one carousel per run.

## Permissions

- Writes: loops/carousel-writing-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/carousel-writing-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly carousel draft. Verification: slide rules hold. Memory: loops/carousel-writing-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
