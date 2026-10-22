---
name: validate-skills
title: Validate Skills skill
repo: callstackincubator/agent-skills
license: MIT
url: https://gethabit.dev/skills/callstackincubator/validate-skills
---

# Validate Skills skill

The validate skills skill checks every skill in a repo against the agentskills.io spec and Claude Code best practices, then reports PASS or FAIL per rule. For people who maintain a repo of agent skills.

- Install the skill: `npx skills add callstackincubator/agent-skills --skill validate-skills`
- Source: https://github.com/callstackincubator/agent-skills/tree/HEAD/.claude/skills/validate-skills
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You maintain a skills repo; You add or rename a skill; You want to lint SKILL.md files.
Skip it when: You have no skills/ folder; You need to test what a skill does, not its format.

# Make it a habit: Every skill passes the spec.

On each pull request that touches skills/, your agent checks every skill folder against the agentskills.io spec and Claude Code best practices: name, description, body length and link rules. It reports PASS or FAIL per check and keeps the last results.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR touches skills folder (event; GitHub Actions or Claude Code routine; `pull_request paths: skills/**`)
- **Verification:** all checks PASS. Hard checks: name field matches the directory name; description is 1 to 1024 characters; SKILL.md body is under 500 lines; every reference file is linked from SKILL.md. On fail: notify, max 0 retries.
- **Memory:** last validation results at `loops/validate-skills-loop/results.md`. Read first: skills that failed last time.

## Steps

1. **Find skill folders.** Your agent lists every skill directory with fd -t d -d 1 . skills/.
2. **Check the spec.** For each SKILL.md it checks name format, name match, description length and optional fields.
3. **Check best practices.** It checks third-person description, body length, markdown links, no repeat of the description and one-level-deep loading.
4. **Report results.** It writes a Validation Results list with PASS or FAIL per check.
5. **Save the log.** It stores the results so the next run can compare.

Stop rule: Stops after all skill folders in skills/ are checked once per run.

## Permissions

- Writes: loops/validate-skills-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/validate-skills-loop/results.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR touches skills folder. Verification: all checks PASS. Memory: loops/validate-skills-loop/results.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
