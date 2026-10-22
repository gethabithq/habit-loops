---
name: book-to-skill
title: Book to Skill skill
repo: virgiliojr94/book-to-skill
license: MIT
url: https://gethabit.dev/skills/virgiliojr94/book-to-skill
---

# Book to Skill skill

The book to skill converter turns PDF, EPUB, DOCX, HTML and Markdown documents into structured agent skills with chapter files, glossary, patterns and a cheatsheet. For readers who want an agent to apply an author's frameworks while working.

- Install the skill: `npx skills add virgiliojr94/book-to-skill --skill book-to-skill`
- Source: https://github.com/virgiliojr94/book-to-skill
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You want a book as an agent skill; You build a reusable knowledge base; You add new sources to a book skill.
Skip it when: You only want a short summary; You plan to publish copyrighted text.

# Make it a habit: Keep book skills up to date.

When you add a new document, your agent extracts it, confirms the source and token estimate with you, then folds it into the existing book skill with new chapters and merged glossary, patterns and cheatsheet. The security scan must pass before the run ends.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** new document added (event; Claude Code routine; `a new PDF, EPUB, DOCX or Markdown file lands in your sources folder`)
- **Verification:** scan passes, you confirm. Hard checks: metadata.json sources match the new file; scan_generated_skill.py exits zero; SKILL.md body stays under 4,000 tokens; every new chapter file is listed in the Chapter Index. On fail: stop, max 0 retries.
- **Memory:** fold-in history at `loops/book-fold-in-loop/log.md`. Read first: which sources were already folded into which skill.

## Steps

1. **Validate input.** Check the new file has a supported format and spot that the target skill already exists, so this is an Update/Fold-in run.
2. **Ask content type.** Ask you whether the source is technical or text-heavy to pick the extraction mode.
3. **Extract.** Run extract.py, then confirm in metadata.json that the extracted file is the one you added.
4. **Confirm estimate.** Show you sources, pages and token counts and wait for your go before generating.
5. **Fold in chapters.** Merge revisions into existing chapter files or add new ones numbered after the highest chapter.
6. **Merge indexes.** Update glossary.md, patterns.md, cheatsheet.md and the Chapter and Topic Index in SKILL.md.
7. **Scan.** Run scan_generated_skill.py and stop for your review if it reports findings.
8. **Clean up.** Remove only this run's workdir and log the folded source.

Stop rule: One new document per run; stop at the first scan finding without rewriting files.

## Permissions

- Writes: ~/.agents/skills/, loops/book-fold-in-loop/
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/book-fold-in-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: new document added. Verification: scan passes, you confirm. Memory: loops/book-fold-in-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
