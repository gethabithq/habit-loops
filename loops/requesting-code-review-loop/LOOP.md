---
name: requesting-code-review
title: Requesting Code Review skill
repo: obra/superpowers
license: MIT
url: https://gethabit.dev/skills/obra/requesting-code-review
---

# Requesting Code Review skill

The requesting code review skill has your agent send its diff to a fresh reviewer subagent with clean context, then fix what it finds by severity. For developers who build with coding agents.

- Install the skill: `npx skills add obra/superpowers --skill requesting-code-review`
- Source: https://github.com/obra/superpowers/tree/HEAD/skills/requesting-code-review
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: a task or feature is finished; before a merge to main; you are stuck on a change.
Skip it when: there is no commit to compare; you review every diff by hand anyway.

# Make it a habit: Every task reviewed before merge.

After each finished task or before a merge to main, your agent sends the diff between two git SHAs to a fresh reviewer subagent. It fixes Critical and Important issues at once and notes Minor ones. The list of open Minor issues is kept for the next run.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** task done or merge (event; GitHub Actions or Claude Code routine; `pull_request opened against main`)
- **Verification:** no open Critical issues. Hard checks: BASE_SHA and HEAD_SHA resolve with git rev-parse; reviewer returns zero Critical issues; reviewer returns zero unfixed Important issues. Critic: claude-opus-5-5, pass at 17/20. On fail: retry, max 2 retries.
- **Memory:** open minor issues at `loops/requesting-code-review-loop/minor.md`. Read first: Minor issues noted in earlier reviews.

## Steps

1. **Get the SHAs.** Find BASE_SHA and HEAD_SHA with git rev-parse or git merge-base.
2. **Dispatch reviewer.** Send a general-purpose subagent the code-reviewer.md template with description, requirements and both SHAs.
3. **Fix Critical issues.** Fix Critical issues at once and Important issues before the next task.
4. **Note Minor issues.** Write Minor issues to the loop notes for later.
5. **Push back if wrong.** If the reviewer is wrong, answer with technical reasons and code or tests.

Stop rule: Stops after one review per task, with at most two fix-and-review rounds.

## Permissions

- Writes: src/**, tests/**, loops/requesting-code-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/requesting-code-review-loop/minor.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: task done or merge. Verification: no open Critical issues. Memory: loops/requesting-code-review-loop/minor.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
