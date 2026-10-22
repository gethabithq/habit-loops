---
name: scope-triage
title: Scope Triage skill
repo: sentimony/skills
license: MIT
url: https://gethabit.dev/skills/sentimony/scope-triage
---

# Scope Triage skill

The scope triage skill helps coding agents decide whether a request can go straight to implementation, needs a light spec, or needs a full design with user approval, using a hypothesis and an assumption ledger.

- Install the skill: `npx skills add sentimony/skills --skill scope-triage`
- Source: https://github.com/sentimony/skills/tree/HEAD/plugins/devflow/skills/scope-triage
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: A request needs design decisions; Success criteria are unclear; Two approaches are possible.
Skip it when: The request is only informational; You continue an already approved design.

# Make it a habit: Every request gets a route first.

When a new request or issue arrives, your agent states a hypothesis with confidence, writes an assumption ledger, checks repository facts and picks Route A, B or C. In unattended runs it proceeds only on Route A and otherwise stops and reports. A log keeps routes.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** new request arrives (event; GitHub Actions or Claude Code routine; `issue opened or new task request`)
- **Verification:** route announced with ledger. Hard checks: a hypothesis with a confidence percentage is stated; every assumption is marked verified, assumed or contradicted; any contradicted entry leads to Route C; no secret value appears in the route sentence or ledger. On fail: stop, max 0 retries.
- **Memory:** route decisions log at `loops/scope-triage-loop/run-log.md`. Read first: earlier routes and blockers for related requests.

## Steps

1. **State hypothesis.** Write one sentence on the wanted result with an honest confidence.
2. **Write the ledger.** List assumptions and verify them with one broad search and targeted reads.
3. **Classify.** Check the conditions for Route A, B and C; any doubt means Route C.
4. **Announce.** Repeat the target contract in one self-contained sentence with the route.
5. **Hand off or stop.** Route A goes to tdd or debugging; in unattended runs anything else stops with the blocker.

Stop rule: Stops after one request per run; unattended runs never start Route C.

## Permissions

- Writes: loops/scope-triage-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/scope-triage-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: new request arrives. Verification: route announced with ledger. Memory: loops/scope-triage-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
