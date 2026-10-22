---
name: typst
title: Typst skill
repo: lucifer1004/claude-skill-typst
license: MIT
url: https://gethabit.dev/skills/lucifer1004/typst
---

# Typst skill

The typst skill helps writers and developers create Typst documents, templates and packages, convert from Markdown or LaTeX and verify output via HTML, PNG or pdftotext.

- Install the skill: `npx skills add lucifer1004/claude-skill-typst --skill typst`
- Source: https://github.com/lucifer1004/claude-skill-typst/tree/HEAD/skills/typst
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You work with .typ files; You convert LaTeX or Markdown to Typst; You build a Typst template or package.
Skip it when: You write in LaTeX only; You need a word processor file.

# Make it a habit: Typst documents always compile cleanly.

Whenever a .typ file changes, your agent runs typst compile, fixes errors using the common error table, checks text and structure through HTML export and layout through PNG export, and notes fixes for the next change.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** .typ file changed (event; Claude Code routine or GitHub Actions; `a commit or save changes a .typ file`)
- **Verification:** compile passes, output checked. Hard checks: typst compile exits without errors; the output PDF exists; HTML export shows the expected headings. On fail: retry, max 2 retries.
- **Memory:** build fixes log at `loops/typst-build-check-loop/run-log.md`. Read first: errors fixed in earlier runs.

## Steps

1. **Compile.** Run typst compile on the changed document, with --root when it uses /path imports.
2. **Fix errors.** Match each error to the common errors table and fix it.
3. **Check text.** Export HTML with --features html to check headings and tables.
4. **Check layout.** Export PNG pages to check alignment, spacing and fonts.
5. **Upgrade old code.** Use migration.md when code predates Typst 0.15.

Stop rule: Stops after one document, with at most 2 fix rounds.

## Permissions

- Writes: **/*.typ, **/*.pdf, loops/typst-build-check-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/typst-build-check-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: .typ file changed. Verification: compile passes, output checked. Memory: loops/typst-build-check-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
