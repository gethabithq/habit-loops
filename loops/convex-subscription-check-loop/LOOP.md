---
name: convex-realtime
title: Convex Realtime skill
repo: waynesutton/builder-skills
license: Apache-2.0
url: https://gethabit.dev/skills/waynesutton/convex-realtime
---

# Convex Realtime skill

The convex realtime skill helps build reactive UIs on Convex subscriptions with useQuery patterns, optimistic updates, live pagination, presence and less subscription churn. For developers wiring a React frontend to Convex.

- Install the skill: `npx skills add waynesutton/builder-skills --skill convex-realtime`
- Source: https://github.com/waynesutton/builder-skills/tree/HEAD/skills/convex-realtime
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: data does not update live; a page rerenders too often; a paginated list drops rows.
Skip it when: the backend is not Convex; you only need server-side code.

# Make it a habit: Live queries stay small and indexed.

When a pull request changes Convex queries or React components that use them, the agent walks the skill's checklist: skip instead of conditional hooks, undefined handled, withIndex reads, no Date.now() in queries, paginate for growing lists. It logs what it found.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR touches convex code (event; GitHub Actions or Claude Code routine; `pull_request paths: convex/**`)
- **Verification:** realtime checklist passes. Hard checks: no Date.now() or Math.random() inside any query; every backend query has args and returns validators; no .filter() on a large table where withIndex fits; no conditional useQuery call, skip is used instead. On fail: notify, max 0 retries.
- **Memory:** query findings log at `loops/convex-subscription-check-loop/log.md`. Read first: queries flagged before and whether they were fixed.

## Steps

1. **Read past findings.** Open the log to see which queries were flagged before.
2. **List changed queries.** Collect the changed query functions and the components that call useQuery or usePaginatedQuery.
3. **Check read sets.** Confirm each query reads through withIndex and bounds results with .take(n) or .paginate().
4. **Check determinism.** Flag any Date.now(), Math.random() or fetch inside a query.
5. **Check client hooks.** Confirm undefined is handled first and conditional queries pass skip.
6. **Check optimistic updates.** Make sure each optimistic update touches every query the mutation changes.
7. **Log the findings.** Write each issue with its file and the fix the checklist suggests.

Stop rule: One pull request per run, at most 20 query functions checked.

## Permissions

- Writes: loops/convex-subscription-check-loop/
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/convex-subscription-check-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR touches convex code. Verification: realtime checklist passes. Memory: loops/convex-subscription-check-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
