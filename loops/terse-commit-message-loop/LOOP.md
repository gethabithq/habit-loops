---
name: caveman-commit
title: Caveman Commit skill
repo: JuliusBrussee/caveman
license: Apache-2.0
url: https://gethabit.dev/skills/juliusbrussee/caveman-commit
---

# Caveman Commit skill

The caveman commit skill writes short Conventional Commits messages that state intent only: imperative subject, allowed type and optional scope, a body only when needed, no filler. For developers who want clean, terse git history.

- Install the skill: `npx skills add JuliusBrussee/caveman --skill caveman-commit`
- Source: https://github.com/JuliusBrussee/caveman/tree/HEAD/skills/caveman-commit
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You want a commit message for staged changes; Your project uses Conventional Commits; You want why over what in history.
Skip it when: You want the agent to run git commit itself; Your project uses a different commit format.

# Make it a habit: Every commit message short and exact.

Whenever you ask for a commit message, your agent reads the staged diff and writes a Conventional Commits message: imperative subject, type and optional scope, a body only when the why, a breaking change or a migration needs it. You paste it; the agent never commits.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** commit message requested (event; Claude Code; `/commit or /caveman-commit`)
- **Verification:** format rules check. Hard checks: subject matches <type>(<scope>): <summary> with an allowed type; subject is at most 72 characters with no trailing period; body lines wrap at 72 characters; breaking changes, security fixes, data migrations and reverts include a body. On fail: retry, max 1 retries.
- **Memory:** past commit messages at `loops/terse-commit-message-loop/notes.md`. Read first: project capitalization and scope conventions from recent commits.

## Steps

1. **Read the diff.** The agent looks at what changed and why.
2. **Pick type and scope.** It picks feat, fix, refactor, perf, docs, test, chore, build, ci, style or revert, plus an optional scope.
3. **Write the subject.** It writes an imperative summary, aiming for 50 characters and never above 72.
4. **Decide on a body.** It adds a body only for a non-obvious why, breaking change, migration note or linked issue.
5. **Strip filler.** It removes phrases like this commit, I or we, emoji, and AI attribution unless your own rule asks for a trailer.
6. **Hand over.** It outputs the message as a code block to paste, without staging or committing.

Stop rule: Stops after one commit message per request.

## Permissions

- Writes: nothing
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/terse-commit-message-loop/notes.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: commit message requested. Verification: format rules check. Memory: loops/terse-commit-message-loop/notes.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
