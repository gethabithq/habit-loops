---
name: cangjie-skill
title: Cangjie Skill skill
repo: kangarooking/cangjie-skill
license: MIT
url: https://gethabit.dev/skills/kangarooking/cangjie-skill
---

# Cangjie Skill skill

The cangjie skill helps readers and teams distill a book, long video transcript, podcast or course into a verified set of executable agent skills, through a staged extraction and testing pipeline.

- Install the skill: `npx skills add kangarooking/cangjie-skill --skill cangjie-skill`
- Source: https://github.com/kangarooking/cangjie-skill
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You turn a book into skills; You distill a course or podcast; You want reusable frameworks from long content.
Skip it when: You want a simple summary; You have no source text.

# Make it a habit: One book distilled into usable skills.

For each book on the board, your agent resumes from PIPELINE_STATE.md, runs the staged pipeline: overview, parallel extraction, triple verification, promotion gate, capability cards, linking, pressure tests and compile. You confirm at each gate.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** next book on board (manual; Claude Code routine; `run when a book text is ready on the board`)
- **Verification:** you confirm, pack validates. Hard checks: each capability passed all three verifications; each capability card has all six sections; scripts/validate_skill_pack.py passes on the compiled output; quotes stay within 150 characters per passage. On fail: stop, max 0 retries.
- **Memory:** pipeline state file at `books/<book-slug>/PIPELINE_STATE.md`. Read first: the current stage and progress for this book.

## Steps

1. **Confirm inputs.** Get the text source, metadata and purpose from you; never distill from memory.
2. **Overview.** Write BOOK_OVERVIEW.md and wait for your confirmation.
3. **Extract.** Run the five extractor prompts, in parallel when possible, into candidates/.
4. **Verify and promote.** Apply the triple verification and the promotion gate, then show you the four groups.
5. **Build cards.** Write capability cards and register them in verified.yaml with links.
6. **Pressure test.** Run representative tasks and rework cards that fail.
7. **Compile.** Run python3 scripts/cangjie.py compile, write DIGEST.md and ask where to install.

Stop rule: Stops after one book per run, pausing at each confirmation gate.

## Permissions

- Writes: books/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`books/<book-slug>/PIPELINE_STATE.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: next book on board. Verification: you confirm, pack validates. Memory: books/<book-slug>/PIPELINE_STATE.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
