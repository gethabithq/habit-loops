---
name: sigma
title: Sigma skill
repo: sanyuan0704/sanyuan-skills
license: MIT
url: https://gethabit.dev/skills/sanyuan0704/sigma
---

# Sigma skill

Sigma is a personal 1-on-1 AI tutor based on Bloom's 2-Sigma mastery learning: it diagnoses your level, teaches by Socratic questions, tracks misconceptions and builds visual roadmaps. For anyone who wants to learn a topic step by step.

- Install the skill: `npx skills add sanyuan0704/sanyuan-skills --skill sigma`
- Source: https://github.com/sanyuan0704/sanyuan-skills/tree/HEAD/skills/sigma
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You want to learn a new topic; You need a concept explained step by step; You want spaced review of a topic.
Skip it when: You only need a quick answer; You do not want to be quizzed.

# Make it a habit: Learned concepts stay learned.

Each day your agent resumes your Sigma session, asks one recall question per mastered concept that is due, doubles or resets its review interval and then continues the roadmap. The session file keeps mastery scores, misconceptions and review dates.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** daily review session (schedule; Claude Code routine; `0 19 * * *`)
- **Verification:** your answers + session update. Hard checks: session.md is updated after every round; roadmap.html is regenerated after every round; no concept is marked mastered without a passed practice task. On fail: retry, max 0 retries.
- **Memory:** session and profile at `sigma/{topic-slug}/session.md`. Read first: sigma/learner-profile.md, then concept statuses, review intervals and open misconceptions.

## Steps

1. **Load memory.** Read sigma/learner-profile.md and the topic's session.md with --resume.
2. **Review due concepts.** Ask one recall question for each mastered concept whose interval has passed, at most 5.
3. **Update intervals.** Double the interval on a correct answer up to 32 days, or reset it to 1 day.
4. **Clear misconceptions.** Address unresolved misconceptions with counter-examples before new content.
5. **Tutor the next concept.** Ask 1 to 2 questions per round, never give answers, and check mastery with the rubric.
6. **Practice and sync.** Give a small practice task before marking mastery and update session.md and roadmap.html.

Stop rule: Stops after at most 5 review questions and one new concept per session.

## Permissions

- Writes: sigma/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`sigma/{topic-slug}/session.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: daily review session. Verification: your answers + session update. Memory: sigma/{topic-slug}/session.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
