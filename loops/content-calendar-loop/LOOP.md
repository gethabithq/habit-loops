---
name: content-calendar-sms
title: Content Calendar skill
repo: blacktwist/social-media-skills
license: MIT
url: https://gethabit.dev/skills/blacktwist/content-calendar-sms
---

# Content Calendar skill

The content calendar skill helps social media creators plan a balanced posting schedule across platforms, with content pillars, flexible slots, a batching plan and optional scheduling through BlackTwist.

- Install the skill: `npx skills add blacktwist/social-media-skills --skill content-calendar-sms`
- Source: https://github.com/blacktwist/social-media-skills/tree/HEAD/skills/content-calendar-sms
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You plan next week's posts; You ask how often to post; You batch content in advance.
Skip it when: You need the post text itself; You have not chosen your content pillars.

# Make it a habit: Next week's posting plan, every Monday.

Every Monday your agent reads your social media context, reviews last week's results, builds a balanced weekly calendar with open slots and a batching plan, and asks you to confirm. With BlackTwist connected it schedules only approved posts.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** Monday planning session (schedule; Claude Code routine; `0 8 * * 1`)
- **Verification:** you confirm the calendar. Hard checks: no pillar fills more than 40% of slots; 20 to 30% of slots are flexible; no active platform goes more than 3 days without a post; every scheduled post was confirmed first. On fail: retry, max 1 retries.
- **Memory:** weekly calendar and review at `loops/content-calendar-loop/calendar.md`. Read first: last week's calendar and review notes.

## Steps

1. **Read context.** Read .agents/social-media-context-sms.md and skip questions it already answers.
2. **Review last week.** Note top and weak posts, using get_post_analytics when BlackTwist is connected.
3. **Build the calendar.** Map pillars to days, platforms and formats, keeping open slots.
4. **Plan batches.** Write a batching plan by platform.
5. **You confirm.** Show the calendar and ask which slots to adjust.
6. **Schedule.** With BlackTwist, use list_time_slots and create_post only for posts you approved.

Stop rule: Stops after one week's calendar per run.

## Permissions

- Writes: loops/content-calendar-loop/**
- Network: none
- Sends: scheduled posts via BlackTwist after your confirmation
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/content-calendar-loop/calendar.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: Monday planning session. Verification: you confirm the calendar. Memory: loops/content-calendar-loop/calendar.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
