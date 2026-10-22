---
name: writing-clearly-and-concisely
title: Writing Clearly and Concisely skill
repo: softaworks/agent-toolkit
license: MIT
url: https://gethabit.dev/skills/softaworks/writing-clearly-and-concisely
---

# Writing Clearly and Concisely skill

Writing clearly and concisely edits prose for humans, from docs and commit messages to error messages and UI text, applying Strunk's Elements of Style rules and removing AI writing patterns. For anyone writing prose people will read.

- Install the skill: `npx skills add softaworks/agent-toolkit --skill writing-clearly-and-concisely`
- Source: https://github.com/softaworks/agent-toolkit/tree/HEAD/dist/plugins/writing-clearly-and-concisely/skills/writing-clearly-and-concisely
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You write docs or a README; You write error or UI copy; You tighten a draft.
Skip it when: You generate code only; You want longer, fancier prose.

# Make it a habit: Human-facing prose reads clear and tight.

When docs, READMEs or UI copy change, your agent edits the prose with Strunk's rules: active voice, positive form, concrete language and no needless words, and strips AI puffery like seamless and leverage. A log keeps recurring wording issues.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** prose files change (event; GitHub Actions or Claude Code routine; `push paths: docs/**, README.md`)
- **Verification:** AI puffery count zero. Hard checks: the changed prose has no banned puffery words such as seamless, robust or leverage; no passive voice remains in step instructions; every paragraph has one topic. On fail: notify, max 1 retries.
- **Memory:** wording issue log at `loops/prose-clarity-edit-loop/log.md`. Read first: recurring puffery and wording issues from earlier edits.

## Steps

1. **Draft the edit.** Make a first pass with judgment on the changed prose.
2. **Load the section.** Read 03-elementary-principles-of-composition.md for active voice, concrete language and concision.
3. **Apply Strunk.** Rewrite for active voice, positive form, concrete words and emphatic words at the end.
4. **Cut AI patterns.** Remove puffery, empty -ing phrases, promotional adjectives and formatting overuse.
5. **Log issues.** Record recurring wording problems for the next run.

Stop rule: Stops after the changed prose of one change, with 1 retry.

## Permissions

- Writes: docs/**, README.md, loops/prose-clarity-edit-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/prose-clarity-edit-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: prose files change. Verification: AI puffery count zero. Memory: loops/prose-clarity-edit-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
