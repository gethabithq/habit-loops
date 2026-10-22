---
name: systematic-debugging
title: Systematic Debugging skill
repo: obra/superpowers
license: MIT
url: https://gethabit.dev/skills/obra/systematic-debugging
---

# Systematic Debugging skill

The systematic debugging skill makes your coding agent find the root cause of a bug before it changes any code. It runs four phases and writes a failing test first. For developers who want fewer symptom patches.

- Install the skill: `npx skills add obra/superpowers --skill systematic-debugging`
- Source: https://github.com/obra/superpowers/tree/HEAD/skills/systematic-debugging
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: a test or build fails; a bug shows up in production; a quick fix already failed.
Skip it when: you only want a new feature; there is no error to investigate.

# Make it a habit: Every bug fixed at its source.

When a test or build fails, your agent works through four phases: root cause, pattern, hypothesis, fix. It writes a failing test first, makes one change, and checks that the whole suite passes. It logs each hypothesis and fix count per bug.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** test or build fails (event; GitHub Actions or Claude Code routine; `CI run status == failure`)
- **Verification:** failing test now passes. Hard checks: a failing test exists before the fix; the new test passes after the fix; no other test in the suite breaks; fewer than 3 fix attempts on this bug. On fail: retry, max 2 retries.
- **Memory:** bug and hypothesis log at `loops/systematic-debugging-loop/log.md`. Read first: past hypotheses and fix attempts for this bug.

## Steps

1. **Investigate root cause.** Read the full error and stack trace, reproduce the failure, and check recent changes with git diff.
2. **Gather evidence.** In systems with many parts, log what enters and leaves each part to find where it breaks.
3. **Compare patterns.** Find similar code that works and list every difference from the broken code.
4. **Test one hypothesis.** Write down one cause, then make the smallest change that tests it.
5. **Write failing test.** Use the superpowers:test-driven-development skill to pin the bug in a test that fails.
6. **Fix and verify.** Make one fix at the source, then use superpowers:verification-before-completion before you call it done.
7. **Escalate after three.** If three fixes failed, stop and discuss the architecture with your human partner.

Stop rule: Stops after one bug per run, or after three failed fix attempts.

## Permissions

- Writes: src/**, tests/**, loops/systematic-debugging-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/systematic-debugging-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: test or build fails. Verification: failing test now passes. Memory: loops/systematic-debugging-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
