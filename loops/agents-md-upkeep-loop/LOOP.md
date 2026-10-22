---
name: agents-md
title: AGENTS.md skill
repo: getsentry/skills
license: Apache-2.0
url: https://gethabit.dev/skills/getsentry/agents-md
---

# AGENTS.md skill

The agents md skill from Sentry creates and maintains short AGENTS.md and CLAUDE.md files with exact commands and doc references. For teams who want coding agents to follow repo rules.

- Install the skill: `npx skills add getsentry/skills --skill agents-md`
- Source: https://github.com/getsentry/skills/tree/HEAD/skills/agents-md
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You set up a new repo for agents; AGENTS.md is long or stale; You want CLAUDE.md and AGENTS.md in sync.
Skip it when: You need full contributor docs; The repo has no build or test commands.

# Make it a habit: Keep agent instructions short, accurate.

Each month your agent inspects lock files, manifests, CI and docs, updates AGENTS.md to the smallest useful file and checks every path and command still exists. Git history keeps each change.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** monthly instructions review (schedule; Claude Code routine; `0 9 1 * *`)
- **Verification:** length and paths check. Hard checks: AGENTS.md is under 100 lines; every listed path exists; every listed command exists in package.json, Makefile or CI; CLAUDE.md is a symlink to AGENTS.md if present. On fail: notify, max 1 retries.
- **Memory:** AGENTS.md git history at `AGENTS.md`. Read first: the last commit that changed AGENTS.md.

## Steps

1. **Inspect the repo.** Your agent reads lock files, package.json, Makefile, CI workflows and docs such as CONTRIBUTING.md.
2. **Choose scope.** It keeps root AGENTS.md for defaults and nested files only where rules differ.
3. **Write small.** It updates only sections that add non-obvious value, in tables and bullets.
4. **Verify.** It checks each path and command really exists.
5. **Commit.** It commits the change so the history shows what moved.

Stop rule: Stops after one root file and up to 3 nested files per run.

## Permissions

- Writes: AGENTS.md, **/AGENTS.md, CLAUDE.md
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`AGENTS.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: monthly instructions review. Verification: length and paths check. Memory: AGENTS.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
