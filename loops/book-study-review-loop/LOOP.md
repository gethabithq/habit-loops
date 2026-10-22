---
name: book-study
title: Book Study skill
repo: sanyuan0704/sanyuan-skills
license: MIT
url: https://gethabit.dev/skills/sanyuan0704/book-study
---

# Book Study skill

Book Study is a reading coach that guides you chapter by chapter: pre-reading questions, knowledge compilation into a wiki, Socratic mastery tests and spaced-repetition review. For people studying books deeply.

- Install the skill: `npx skills add sanyuan0704/sanyuan-skills --skill book-study`
- Source: https://github.com/sanyuan0704/sanyuan-skills/tree/HEAD/skills/book-study
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: studying a book systematically; reviewing what you read with spaced repetition; being quizzed on a chapter.
Skip it when: you want a quick skim, not deep study; you will not revisit the material.

# Make it a habit: Book concepts held in long-term memory.

Each session, your agent checks the mastery map for due items, reviews them with Socratic questions, then guides the next chapter: pre-reading questions, ingest, mastery test and practice. The mastery-map.md keeps what is due.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** you open the book (manual; Claude Code routine; `/book-study <book-name>`)
- **Verification:** mastery before advancing. Hard checks: due review items are handled before a new chapter; a concept is marked mastered only after a passed practice task; study-plan.md and mastery-map.md are updated. On fail: notify, max 0 retries.
- **Memory:** mastery map at `book-wiki/<book-slug>/mastery-map.md`. Read first: the mastery map for what is mastered and what is due for review.

## Steps

1. **Restore state.** Your agent reads study-plan.md and mastery-map.md to see where you left off and what is due.
2. **Review due items.** It reviews due knowledge points first with one Socratic question each, resetting failed items.
3. **Pre-reading guide.** It sets two or three pre-reading questions tied to your goal before you read the chapter.
4. **Ingest.** It compiles your notes into concepts, cases, models, quotes and questions pages.
5. **Mastery test.** It tests with the four-criterion rubric and the mastery threshold before advancing.
6. **Practice.** It requires a small application task before marking a concept mastered.

Stop rule: Stops after one chapter cycle or review session per run.

## Permissions

- Writes: book-wiki/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`book-wiki/<book-slug>/mastery-map.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: you open the book. Verification: mastery before advancing. Memory: book-wiki/<book-slug>/mastery-map.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
