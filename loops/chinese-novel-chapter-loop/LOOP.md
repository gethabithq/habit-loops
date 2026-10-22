---
name: chinese-novelist
title: Chinese Novelist skill
repo: penglonghuang/chinese-novelist-skill
license: MIT
url: https://gethabit.dev/skills/penglonghuang/chinese-novelist
---

# Chinese Novelist skill

The chinese novelist skill writes full Chinese novels in any genre: layered questions, outline and plan, chapter-by-chapter writing with hooks, resume after a stop and automatic length and quality checks. For writers of serial fiction.

- Install the skill: `npx skills add penglonghuang/chinese-novelist-skill --skill chinese-novelist`
- Source: https://github.com/penglonghuang/chinese-novelist-skill
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You want a long Chinese novel; You need to resume an unfinished novel; You want chapter-by-chapter fiction.
Skip it when: You need English fiction; You want a short poem.

# Make it a habit: Write a novel chapter by chapter.

Your agent asks about genre, hero and conflict, plans an outline and writing plan you confirm, then writes chapters from the outline, resumes where it stopped and checks length and quality, rewriting weak chapters up to 3 rounds.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** you start or resume (manual; Claude Code routine; `user asks to write or continue a novel`)
- **Verification:** you confirm plan, checks. Hard checks: every planned chapter file exists; each chapter meets the word count check; 02-写作计划.json shows every chapter done. On fail: retry, max 2 retries.
- **Memory:** writing plan JSON at `./chinese-novelist/{timestamp}-{title}/02-写作计划.json`. Read first: the writing plan and outline in 01-大纲.md.

## Steps

1. **Load and resume.** Your agent reads your preferences and checks for an unfinished novel to continue.
2. **Ask in layers.** It asks about genre, hero and core conflict, then world, tone and chapter count.
3. **Pick a title.** It suggests titles and you choose or write your own.
4. **Plan and confirm.** It writes the outline, character files and writing plan, and waits for your OK.
5. **Choose the mode.** It writes serially, with parallel subagents, or with agent teams.
6. **Write chapters.** It writes each chapter from its outline entry, with conflict and an end hook.
7. **Check and fix.** It checks every chapter's length and quality and rewrites weak ones.

Stop rule: Stops when all planned chapters pass, after at most 3 fix rounds.

## Permissions

- Writes: ./chinese-novelist/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`./chinese-novelist/{timestamp}-{title}/02-写作计划.json`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: you start or resume. Verification: you confirm plan, checks. Memory: ./chinese-novelist/{timestamp}-{title}/02-写作计划.json. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
