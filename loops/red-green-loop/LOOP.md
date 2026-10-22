---
name: tdd
title: TDD skill
repo: mattpocock/skills
license: MIT
url: https://gethabit.dev/skills/mattpocock/tdd
---

# TDD skill

The tdd skill by mattpocock is a reference for test-driven development: what makes a good test, where seams go, the anti-patterns and the rules of the red green loop. For developers who build test-first.

- Install the skill: `npx skills add mattpocock/skills --skill tdd`
- Source: https://github.com/mattpocock/skills/tree/HEAD/skills/engineering/tdd
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You build a feature test-first; You fix a bug with a test; You want integration tests.
Skip it when: You only prototype; The project has no test runner.

# Make it a habit: Features built test-first, slice by slice.

When a feature or bug is ready, your agent agrees the test seams with you, then works one vertical slice at a time: a failing test, then just enough code to pass. Tests must go red, then green. A board keeps agreed seams and finished slices.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** you start a feature (manual; Claude Code routine; `user asks to build a feature or fix a bug test-first`)
- **Verification:** red then green. Hard checks: the new test fails before the code change; the full test suite passes after the change; every test sits at a seam you confirmed. On fail: retry, max 2 retries.
- **Memory:** seams and slices board at `loops/red-green-loop/board.md`. Read first: confirmed seams and the slices still open.

## Steps

1. **Read the domain.** Your agent reads GLOSSARY.md if it exists and respects ADRs in the area.
2. **Agree the seams.** It proposes the public seams to test, each with what it catches and misses, and you confirm.
3. **Check the interface.** When the interface shape is unclear, it calls the codebase design skill for the vocabulary.
4. **Red.** It writes one failing test at a confirmed seam.
5. **Green.** It writes only enough code to make that test pass.
6. **Next slice.** It marks the slice done on the board and starts the next one.
7. **Hand to review.** Refactoring waits for the review stage with the code review skill.

Stop rule: Stops after 5 slices per run or 2 failed tries to turn one test green.

## Permissions

- Writes: test files, source files, loops/red-green-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/red-green-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: you start a feature. Verification: red then green. Memory: loops/red-green-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
