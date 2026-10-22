---
name: convex-best-practices
title: Convex Best Practices skill
repo: waynesutton/builder-skills
license: Apache-2.0
url: https://gethabit.dev/skills/waynesutton/convex-best-practices
---

# Convex Best Practices skill

Convex best practices covers the production patterns the convex eslint plugin enforces: validators, index reads, idempotent mutations, avoiding OCC write conflicts, pagination, thin wrappers and error handling. For reviewing and fixing Convex code.

- Install the skill: `npx skills add waynesutton/builder-skills --skill convex-best-practices`
- Source: https://github.com/waynesutton/builder-skills/tree/HEAD/skills/convex-best-practices
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You review Convex functions; You fix write conflicts or slow queries; You set up the Convex ESLint plugin.
Skip it when: The project does not use Convex; You want general JavaScript style rules.

# Make it a habit: Convex changes checked against the rules.

On pull requests that touch the convex folder, your agent reviews the code against the production rules, validators on every function, index reads instead of filters, idempotent mutations, ConvexError for client messages, then runs the ESLint plugin and reports failures against the checklist.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** convex code changes (event; GitHub Actions or Claude Code routine; `pull_request paths: convex/**`)
- **Verification:** lint passes, checklist met. Hard checks: every function has args and returns validators; every table read uses withIndex, never .filter(); no Date.now() is used inside a query; npm run lint with the convex eslint plugin passes. On fail: notify, max 1 retries.
- **Memory:** review log at `loops/convex-review-loop/log.md`. Read first: recurring issues flagged before.

## Steps

1. **Scope the diff.** Find the changed functions and schema in the convex folder.
2. **Check reads and writes.** Confirm index reads over filters, idempotent mutations and Promise.all for independent writes.
3. **Check safety rules.** Confirm ConvexError for client messages, internal.* scheduled targets and no Date.now() in queries.
4. **Run the linter.** Run npm run lint with the convex eslint plugin to catch old syntax and missing validators.
5. **Report against the checklist.** List failures against the checklist and log recurring issues.

Stop rule: Stops after the changed convex files of one pull request are reviewed.

## Permissions

- Writes: loops/convex-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/convex-review-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: convex code changes. Verification: lint passes, checklist met. Memory: loops/convex-review-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
