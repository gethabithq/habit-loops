---
name: asd-ste100
title: ASD-STE100 skill
repo: danyuchn/asd-ste100-skill
license: MIT
url: https://gethabit.dev/skills/danyuchn/asd-ste100
---

# ASD-STE100 skill

The ASD-STE100 skill rewrites error messages, tool descriptions and agent instructions into Simplified Technical English, with a linter for sentence length, semicolons and phrasal verbs. For teams whose text is read by other agents.

- Install the skill: `npx skills add danyuchn/asd-ste100-skill --skill asd-ste100`
- Source: https://github.com/danyuchn/asd-ste100-skill
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You write tool descriptions or prompts; Error messages read as vague; Another agent parses your text.
Skip it when: You write marketing copy; You need certified aerospace STE.

# Make it a habit: Keep agent-facing text unambiguous.

When error messages, tool descriptions or prompts change, your agent runs ste-lint.py on them, rewrites flagged sentences in Simplified Technical English while keeping every hedge and fact, and re-runs the linter. A log keeps the baseline count.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** agent-facing text changes (event; GitHub Actions or Claude Code routine; `pull request touches prompts, tool descriptions or error strings`)
- **Verification:** ste-lint passes. Hard checks: scripts/ste-lint.py exits 0 within --baseline; no semicolons in rewritten text; ste-lint.py --selftest passes. On fail: retry, max 2 retries.
- **Memory:** lint baseline log at `loops/ste-plain-text-loop/runs.md`. Read first: the last baseline count and kept-as-is phrases.

## Steps

1. **Pick the mode.** Your agent picks Strict for procedures and errors, STE-flavored for READMEs and changelogs.
2. **Read for meaning.** It reads the text once before changing anything.
3. **Lint.** It runs scripts/ste-lint.py with --json on the changed files.
4. **Rewrite.** It fixes each flagged sentence and keeps hedges, numbers and safety conditions.
5. **Flag trade-offs.** It adds a Kept as-is line where precision needs a longer phrase.
6. **Re-lint.** It runs the linter again and records the new count.

Stop rule: Stops after 20 files or 2 rewrite retries per run.

## Permissions

- Writes: docs/**, loops/ste-plain-text-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/ste-plain-text-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: agent-facing text changes. Verification: ste-lint passes. Memory: loops/ste-plain-text-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
