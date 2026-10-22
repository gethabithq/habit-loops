---
name: genshijin-commit
title: Genshijin Commit skill
repo: interfacex-co-jp/genshijin
license: MIT
url: https://gethabit.dev/skills/interfacex-co-jp/genshijin-commit
---

# Genshijin Commit skill

The genshijin commit skill writes very short Conventional Commits messages in Japanese or English, with the reason first and a body only when it adds context. For developers who want a clean, readable git history.

- Install the skill: `npx skills add interfacex-co-jp/genshijin --skill genshijin-commit`
- Source: https://github.com/interfacex-co-jp/genshijin/tree/HEAD/skills/genshijin-commit
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: you have staged changes and need a message; your repo uses Conventional Commits; you want messages that say why, not what.
Skip it when: you want the agent to run git commit itself; your team uses a different commit format.

# Make it a habit: Short commit messages that explain why.

When changes are staged, your agent writes a Conventional Commits message with genshijin commit: a short imperative subject, a body only when the reason is not obvious. A check tests subject length, type and banned phrases. Notes keep the repo's language and scopes.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** changes are staged (event; Claude Code routine; `staged changes or /genshijin-commit`)
- **Verification:** subject and body rules. Hard checks: subject stays within 72 characters; type is one of feat, fix, refactor, perf, docs, test, chore, build, ci, style, revert; subject has no trailing period; breaking, security, migration and revert commits have a body; no AI attribution line in the message. On fail: retry, max 2 retries.
- **Memory:** repo commit style at `loops/genshijin-commit-loop/style.md`. Read first: the language and scopes the repo uses, taken from git log.

## Steps

1. **Read the history.** The agent checks git log to match the language of earlier commits.
2. **Read the diff.** It looks at the staged change and picks a type and an optional scope.
3. **Write the subject.** It writes one imperative summary, aiming for 50 characters, without a period.
4. **Add a body if needed.** It explains a non-obvious reason, breaking change, migration note or issue reference like Closes #42.
5. **Check the rules.** Length, type, banned phrases and the required body cases are tested; a failing message is rewritten.
6. **Hand it over.** The message comes back in a code block, and the style notes get updated.

Stop rule: Stops after one message per staged change, with at most 2 rewrites.

## Permissions

- Writes: loops/genshijin-commit-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/genshijin-commit-loop/style.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: changes are staged. Verification: subject and body rules. Memory: loops/genshijin-commit-loop/style.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
