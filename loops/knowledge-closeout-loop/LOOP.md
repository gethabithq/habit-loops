---
name: neat-freak
title: Neat Freak skill
repo: kkkkhazix/khazix-skills
license: MIT
url: https://gethabit.dev/skills/kkkkhazix/neat-freak
---

# Neat Freak skill

Neat freak closes out a work session by reconciling project docs, CLAUDE.md or AGENTS.md rules, allowed agent memory and leftover files with what the code and runtime actually do. For developers who want the next session or teammate to start clean.

- Install the skill: `npx skills add kkkkhazix/khazix-skills --skill neat-freak`
- Source: https://github.com/kkkkhazix/khazix-skills/tree/HEAD/neat-freak
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: Docs no longer match the code; You hand a project to someone else; Your CLAUDE.md is stale.
Skip it when: You are in the middle of coding; You want to tidy data or prose files.

# Make it a habit: Docs, rules and code agree.

After each merged change, your agent runs the neat-freak closeout: it inventories the project with audit-inventory.sh, aligns README, docs and CLAUDE.md or AGENTS.md with the actual code, lists leftover session files as delete candidates and reports. Nothing is deleted until you confirm.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** change merged (event; Claude Code routine; `pull_request.closed && merged`)
- **Verification:** fact surfaces + your confirmation. Hard checks: every fact surface has a status such as verified-current, pending or not-applicable; no file was deleted before your confirmation; the project's existing lint, test or build gates pass. On fail: notify, max 0 retries.
- **Memory:** project rules file at `CLAUDE.md`. Read first: the project's one-line purpose, run commands, stack, conventions and current status.

## Steps

1. **Pick the path.** Use the light path for small solo projects and the full path when release flows or multiple platforms are involved.
2. **Inventory.** Run bash scripts/audit-inventory.sh on the project root, or do the same checks by hand.
3. **Align facts.** Compare docs with current code for commands, ports, dependencies and features, fixing stale text in place.
4. **Fix the rules file.** Create a short rules file if none exists, or fix only contradictions in the existing one.
5. **List leftovers.** List finished plan files, debug scripts and old copies as delete candidates with reasons.
6. **Report and wait.** Report impact, changes, candidates and pending items, then clean up only after you confirm.

Stop rule: Stops after one closeout report per merge; cleanup runs only in a second step after your yes.

## Permissions

- Writes: README.md, docs/**, CLAUDE.md, AGENTS.md
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`CLAUDE.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: change merged. Verification: fact surfaces + your confirmation. Memory: CLAUDE.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
