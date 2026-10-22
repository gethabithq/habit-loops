---
name: analyzing-user-feedback
title: Analyzing User Feedback skill
repo: refoundai/lenny-skills
license: MIT
url: https://gethabit.dev/skills/refoundai/analyzing-user-feedback
---

# Analyzing User Feedback skill

The analyzing user feedback skill helps product teams turn large amounts of feedback into confident decisions: group signals into themes, check representation, set up dogfooding and use LLMs to synthesize transcripts and tickets.

- Install the skill: `npx skills add refoundai/lenny-skills --skill analyzing-user-feedback`
- Source: https://github.com/refoundai/lenny-skills/tree/HEAD/skills/analyzing-user-feedback
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: you have piles of user feedback; a loud group demands a feature; you want a dogfooding process.
Skip it when: you have no user feedback yet; you need a survey tool.

# Make it a habit: Turn feedback into clear decisions.

Every week your agent groups new user feedback into themes, checks whether each theme is broad or just loud, and asks you a few sharp questions. A themes file keeps the history so trends and closed loops are easy to track.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly feedback review (schedule; Claude Code routine; `0 9 * * 1`)
- **Verification:** themes checked, you decide. Hard checks: count of feedback items processed above zero; every theme lists how many items support it; every theme has a representation note; themes file updated with this week's date. On fail: notify, max 0 retries.
- **Memory:** feedback themes file at `loops/user-feedback-synthesis-loop/themes.md`. Read first: last week's themes, decisions and users to follow up with.

## Steps

1. **Read past themes.** The agent opens the themes file to see what was open last week.
2. **Categorize signals.** It groups new feedback into themes by segment, frequency and user influence.
3. **Check representation.** For each theme it estimates how much of the user base it reflects, to avoid building for a vocal minority.
4. **Ask key questions.** It asks you a few questions, such as whether you have felt this friction yourself.
5. **Flag closed loops.** Shipped fixes get a reminder to follow up with the users who asked.
6. **Save the themes.** Themes, counts and your decisions go into the themes file.

Stop rule: Stops after one weekly batch and at most 10 themes per run.

## Permissions

- Writes: loops/user-feedback-synthesis-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/user-feedback-synthesis-loop/themes.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly feedback review. Verification: themes checked, you decide. Memory: loops/user-feedback-synthesis-loop/themes.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
