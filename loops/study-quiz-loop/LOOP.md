---
name: tutor
title: Tutor skill
repo: bevibing/tutor-skills
license: MIT
url: https://gethabit.dev/skills/bevibing/tutor
---

# Tutor skill

The tutor skill helps learners using an Obsidian StudyVault take quizzes, drill weak areas and track progress at the concept level with a compact dashboard.

- Install the skill: `npx skills add bevibing/tutor-skills --skill tutor`
- Source: https://github.com/bevibing/tutor-skills/tree/HEAD/skills/tutor
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You want to be quizzed on your notes; You drill weak areas; You check learning progress.
Skip it when: You have no StudyVault folder; You want explanations without quizzes.

# Make it a habit: Find and fix your blind spots.

Each day your agent reads the StudyVault dashboard, asks you which session to run, builds four hint-free questions, grades your answers and updates the concept files and dashboard. Weak concepts come back in new wording next time.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** daily study session (schedule; Claude Code routine; `0 19 * * *`)
- **Verification:** you answer, files update. Hard checks: exactly 4 questions with 4 options each; every answered concept appears in its concepts/{area}.md table; dashboard rates match the concept file sums. On fail: retry, max 1 retries.
- **Memory:** StudyVault dashboard at `StudyVault/concepts/`. Read first: dashboard proficiency table and unresolved concepts.

## Steps

1. **Find the vault.** Locate StudyVault and its dashboard, or stop if none exists.
2. **Ask session type.** Offer diagnostic, drill weak areas, choose a section or hard-mode review, and wait for your pick.
3. **Build questions.** Read references/quiz-rules.md and the section files, then write 4 questions.
4. **Quiz and grade.** Ask the questions, show a results table and explain wrong answers.
5. **Update files.** Update the concept file rows and error notes, then the dashboard stats.

Stop rule: Stops after one 4-question session per run.

## Permissions

- Writes: StudyVault/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`StudyVault/concepts/`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: daily study session. Verification: you answer, files update. Memory: StudyVault/concepts/. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
