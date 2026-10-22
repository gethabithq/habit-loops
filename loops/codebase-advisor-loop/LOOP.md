---
name: improve
title: Improve skill
repo: shadcn/improve
license: MIT
url: https://gethabit.dev/skills/shadcn/improve
---

# Improve skill

The improve skill audits a codebase as a read-only senior advisor and writes ranked, self-contained plans for other agents to execute. For teams who want clear handoff plans for bugs, security, tests and tech debt.

- Install the skill: `npx skills add shadcn/improve --skill improve`
- Source: https://github.com/shadcn/improve/tree/HEAD/skills/improve
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You want an audit of a codebase; You need plans for another agent; You ask where to take the project next.
Skip it when: You want the code fixed right now; The repo is a tiny script.

# Make it a habit: Fresh improvement plans every week.

Each week your agent runs improve in reconcile mode, then a quick audit: it checks done and blocked plans, finds new high-leverage issues, vets them and writes self-contained plans in plans/. It never edits source code. The plans index is the memory.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly code audit (schedule; Claude Code routine; `0 8 * * 1`)
- **Verification:** plans checked, you pick. Hard checks: no file outside plans/ was changed; every finding cites file:line evidence; every plan stamps the git rev-parse commit. On fail: stop, max 0 retries.
- **Memory:** plans index at `plans/README.md`. Read first: plan status, dependencies and rejected findings.

## Steps

1. **Reconcile.** Verify done plans, look into blocked ones and refresh drifted ones.
2. **Recon.** Read README, config, CI and design docs, and note build, test and lint commands.
3. **Audit.** Run a quick audit on correctness, security and tests with read-only subagents.
4. **Vet findings.** Open each cited file, drop by-design items and record rejections.
5. **Ask which to plan.** Show the ranked table and ask you which findings become plans.
6. **Write plans.** Write self-contained plans in plans/ and update plans/README.md.

Stop rule: Stops after the top 6 findings and at most 5 new plans per run.

## Permissions

- Writes: plans/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`plans/README.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly code audit. Verification: plans checked, you pick. Memory: plans/README.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
