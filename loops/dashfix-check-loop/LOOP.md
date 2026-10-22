---
name: dashfix
title: Dashfix skill
repo: sentimony/skills
license: MIT
url: https://gethabit.dev/skills/sentimony/dashfix
---

# Dashfix skill

The dashfix skill helps teams keep project prose free of typographic dashes in any language, with a write mode, a read-only audit, a single-file check and a commit-msg hook.

- Install the skill: `npx skills add sentimony/skills --skill dashfix`
- Source: https://github.com/sentimony/skills/tree/HEAD/plugins/writing/skills/dashfix
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You write docs or UI copy; You audit dash usage in a repo; You want a commit hook against em dashes.
Skip it when: Your style guide requires typographic dashes; You scan binary or generated files.

# Make it a habit: Prose uses only the plain hyphen.

On every pull request with prose changes, your agent runs the single-file dash check on each changed doc, fixes banned dashes with a spaced hyphen or better punctuation, re-runs the check and reports counts. The bundled commit-msg hook guards commit messages.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** prose files changed (event; GitHub Actions or Claude Code routine; `pull_request touches docs, READMEs or UI copy`)
- **Verification:** no banned dashes remain. Hard checks: rg -nP '[\x{2010}-\x{2015}\x{2212}]' finds no replace-verdict hits in changed files; every data or justified hit names its reason; the commit-msg hook exists and matches the bundled script. On fail: retry, max 1 retries.
- **Memory:** dash check log at `loops/dashfix-check-loop/run-log.md`. Read first: files with justified exceptions and earlier counts.

## Steps

1. **Check each file.** Run the rg single-file check on each changed prose file.
2. **Give verdicts.** Mark each hit replace, data or justified.
3. **Fix.** Replace with a spaced hyphen or the punctuation the relation needs, then run the preservation check.
4. **Re-check.** Run the check again and report how many were found and fixed.
5. **Guard commits.** Install scripts/commit-msg if missing, never over a different hook.

Stop rule: Stops after the changed files of one pull request; full-repo fixes only after an audit you request.

## Permissions

- Writes: **/*.md, .git/hooks/commit-msg, loops/dashfix-check-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/dashfix-check-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: prose files changed. Verification: no banned dashes remain. Memory: loops/dashfix-check-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
