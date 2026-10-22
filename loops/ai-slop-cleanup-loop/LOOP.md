---
name: ai-slop-cleaner
title: AI Slop Cleaner skill
repo: yeachan-heo/oh-my-claudecode
license: MIT
url: https://gethabit.dev/skills/yeachan-heo/ai-slop-cleaner
---

# AI Slop Cleaner skill

AI Slop Cleaner cleans AI-generated code with a regression-safe, deletion-first workflow: lock behavior, plan, then remove dead code, duplication and needless abstraction, with an optional reviewer-only mode. For developers tidying AI-built code.

- Install the skill: `npx skills add yeachan-heo/oh-my-claudecode --skill ai-slop-cleaner`
- Source: https://github.com/yeachan-heo/oh-my-claudecode/tree/HEAD/skills/ai-slop-cleaner
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: cleaning bloated or repetitive AI code; removing dead code and wrapper layers; a reviewer-only anti-slop pass.
Skip it when: the task is a new feature or redesign; behavior is too unclear to protect with tests.

# Make it a habit: Bloated AI code trimmed, behavior kept.

After AI-written code lands, your agent locks behavior with regression tests, writes a cleanup plan, then runs deletion-first passes for dead code, duplication, naming and tests, keeping the gates green. A run log keeps what was cleaned.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** after AI code lands (event; Claude Code routine; `a changed-file set to clean`)
- **Verification:** gates green, behavior kept. Hard checks: regression tests pass before and after each pass; lint and typecheck for the touched area pass; the diff removes dead code or duplication, not just adds. On fail: retry, max 2 retries.
- **Memory:** cleanup log at `loops/ai-slop-cleanup-loop/run-log.md`. Read first: the cleanup plan and the smells cleaned last run.

## Steps

1. **Protect behavior.** Your agent identifies what must stay the same and adds the narrowest regression tests first.
2. **Write the plan.** It bounds the pass to the given files and lists the concrete smells to remove, safest first.
3. **Classify slop.** It classifies duplication, dead code, needless abstraction, boundary leaks and missing tests.
4. **Delete first.** It runs one smell-focused pass at a time, dead code, then duplicates, then naming, then tests.
5. **Run gates.** It keeps regression tests green and runs lint, typecheck and the touched area's tests after each pass.
6. **Report.** It reports changed files, simplifications, the verification run and remaining risks.

Stop rule: Stops after the bounded file scope is cleaned, with at most 2 retries; it does not expand scope on its own.

## Permissions

- Writes: the files in the cleanup scope, loops/ai-slop-cleanup-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/ai-slop-cleanup-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: after AI code lands. Verification: gates green, behavior kept. Memory: loops/ai-slop-cleanup-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
