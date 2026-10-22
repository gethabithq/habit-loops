---
name: tutor-setup
title: Tutor Setup skill
repo: bevibing/tutor-skills
license: MIT
url: https://gethabit.dev/skills/bevibing/tutor-setup
---

# Tutor Setup skill

The tutor setup skill helps learners and teams turn PDFs, text, web pages or a codebase into an Obsidian StudyVault with concept notes, practice questions, dashboards and links.

- Install the skill: `npx skills add bevibing/tutor-skills --skill tutor-setup`
- Source: https://github.com/bevibing/tutor-skills/tree/HEAD/skills/tutor-setup
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You turn course PDFs into study notes; You build an onboarding vault for a codebase; You want practice questions from sources.
Skip it when: You do not use Obsidian; Your sources sit outside the working folder.

# Make it a habit: Sources turned into a study vault.

When new study sources or a codebase arrive in the working folder, your agent detects the mode, asks you to confirm it, maps sources, builds or extends the StudyVault with notes, practice questions and links, and runs the quality checklist.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** new sources added (event; Claude Code routine; `new PDF, text or source files appear in the working folder`)
- **Verification:** you confirm, checklist passes. Hard checks: every topic folder has a practice file with 8 or more questions; every concept note has source_pdf, part and keywords frontmatter; the quality-checklist.md self-review passes; no file outside the working folder was read. On fail: retry, max 2 retries.
- **Memory:** StudyVault dashboard at `StudyVault/00-Dashboard/`. Read first: the MOC topic map and verified source mapping.

## Steps

1. **Detect mode.** Check project markers, pick Document or Codebase mode and ask you to confirm.
2. **Extract sources.** Convert PDFs with pdftotext and read the text, never the raw PDF.
3. **Map sources.** Build a verified source-to-topic mapping and show it to you.
4. **Analyze.** List every topic and subtopic and define the tag registry.
5. **Build the vault.** Create dashboard, concept notes and practice questions per references/templates.md.
6. **Interlink and review.** Cross-link notes and run the quality checklist until it passes.

Stop rule: Stops after one batch of sources per run, with at most 2 fix rounds.

## Permissions

- Writes: StudyVault/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`StudyVault/00-Dashboard/`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: new sources added. Verification: you confirm, checklist passes. Memory: StudyVault/00-Dashboard/. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
