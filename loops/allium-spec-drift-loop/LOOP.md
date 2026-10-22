---
name: weed
title: Weed skill
repo: juxt/allium
license: MIT
url: https://gethabit.dev/skills/juxt/weed
---

# Weed skill

The weed skill compares Allium specifications with implementation code, finds where they diverged, classifies each divergence and helps resolve it, for teams that keep specs and code in sync.

- Install the skill: `npx skills add juxt/allium --skill weed`
- Source: https://github.com/juxt/allium/tree/HEAD/skills/weed
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: auditing spec drift; checking whether code matches the spec; syncing a spec with current code.
Skip it when: no spec exists yet; writing new spec behaviour.

# Make it a habit: Spec and code stay aligned.

Every week, your agent compares the .allium specs with the implementation in check mode and reports each divergence with its spec and code location and a proposed classification. Findings and their status are kept in a run log.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly drift check (schedule; Claude Code routine or GitHub Actions; `0 7 * * 1`)
- **Verification:** check + you classify. Hard checks: allium check passes on all specs; every divergence names a spec file:line and a code file:line; every divergence has one of four classifications; tests pass after any code update. On fail: notify, max 0 retries.
- **Memory:** divergence log at `loops/allium-spec-drift-loop/log.md`. Read first: divergences still open from the last run.

## Steps

1. **Start up.** Your agent reads the language reference and the .allium files, then runs allium check.
2. **Read the code.** It finds the implementation for each entity, rule and trigger.
3. **Compare both ways.** It flags what the spec says but code skips, and what code does that the spec omits.
4. **Check the process.** It checks transition reachability, trigger coverage, undeclared transitions and invariant enforcement.
5. **Analyse.** If available, allium analyse finds process gaps the comparison misses.
6. **Classify.** Each divergence gets a proposed class, and you confirm or override it.

Stop rule: Stops after one check pass over all specs per run; no edits in check mode.

## Permissions

- Writes: loops/allium-spec-drift-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/allium-spec-drift-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly drift check. Verification: check + you classify. Memory: loops/allium-spec-drift-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
