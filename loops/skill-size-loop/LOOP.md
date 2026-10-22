---
name: create-skill
title: Create Skill skill
repo: siviter-xyz/dot-agent
license: MIT
url: https://gethabit.dev/skills/siviter-xyz/create-skill
---

# Create Skill skill

The create skill guide helps agent authors write effective skills: a SKILL.md under 200 lines with name and description frontmatter, plus scripts, references and assets loaded on demand.

- Install the skill: `npx skills add siviter-xyz/dot-agent --skill create-skill`
- Source: https://github.com/siviter-xyz/dot-agent/tree/HEAD/skills/create-skill
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You write a new agent skill; A SKILL.md has grown too long; You split a skill into references.
Skip it when: You only use skills; You need a full test harness.

# Make it a habit: Your skills stay short and loadable.

When a SKILL.md changes, your agent counts its lines against the 200-line rule, checks the frontmatter for name and description and confirms that linked scripts, references and assets exist. Line counts go into a run log.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** a SKILL.md changes (event; GitHub Actions or Claude Code routine; `push touching **/SKILL.md`)
- **Verification:** under 200 lines, valid. Hard checks: SKILL.md is under 200 lines; the YAML frontmatter has name and description; every file linked from SKILL.md exists under references/, scripts/ or assets/. On fail: notify, max 0 retries.
- **Memory:** skill size log at `loops/skill-size-loop/runs.md`. Read first: skills checked before and their line counts.

## Steps

1. **Find changed skills.** Collect every SKILL.md touched by the push.
2. **Count lines.** Each SKILL.md must stay under 200 lines.
3. **Check frontmatter.** The YAML block needs both name and description.
4. **Check resources.** Links must point to files that exist in references/, scripts/ or assets/.
5. **Suggest splits.** For files over the limit, propose which sections move into references/.
6. **Log results.** Line counts and open issues go into the run log.

Stop rule: Stops after ten SKILL.md files per run.

## Permissions

- Writes: loops/skill-size-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/skill-size-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: a SKILL.md changes. Verification: under 200 lines, valid. Memory: loops/skill-size-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
