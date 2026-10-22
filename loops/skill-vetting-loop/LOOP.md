---
name: skill-vetter
title: Skill Vetter skill
repo: UseAI-pro/openclaw-skills-security
license: MIT
url: https://gethabit.dev/skills/useai-pro/skill-vetter
---

# Skill Vetter skill

The skill vetter skill checks a skill before you install it: metadata, permission scope, red-flag patterns like credential paths or prompt injection, and typosquatting, and gives a safe, warning, danger or block verdict.

- Install the skill: `npx skills add UseAI-pro/openclaw-skills-security --skill skill-vetter`
- Source: https://github.com/UseAI-pro/openclaw-skills-security/tree/HEAD/skills/skill-vetter
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You are about to install a new skill; You review a SKILL.md from GitHub; You audit skills you already have.
Skip it when: You only use skills you wrote; You need a full code audit of scripts.

# Make it a habit: Every skill vetted before install.

Whenever a new or updated skill is about to be installed, your agent vets its SKILL.md: metadata, permission scope, red-flag content and typosquatting. It writes a report with a verdict and keeps every report so version changes get vetted again.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** Skill install or update (event; Claude Code routine or GitHub Actions; `new or changed SKILL.md before install`)
- **Verification:** report with verdict. Hard checks: the report has a VERDICT of SAFE, WARNING, DANGER or BLOCK; RED FLAGS count is stated; a skill with network plus shell is flagged; any critical red flag sets the verdict to BLOCK. On fail: stop, max 0 retries.
- **Memory:** vetting reports at `loops/skill-vetting-loop/reports.md`. Read first: past verdicts and the version each was given for.

## Steps

1. **Check metadata.** The agent checks name, semver version, description and author in the frontmatter.
2. **Score permissions.** It rates fileRead, fileWrite, network and shell against what the skill needs.
3. **Scan content.** It looks for critical, warning and informational red flags in the body.
4. **Check typosquats.** It compares the name with known skills for small spelling tricks.
5. **Write the report.** It fills the vetting report format with a verdict and a recommendation.

Stop rule: Stops after one skill per run.

## Permissions

- Writes: loops/skill-vetting-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/skill-vetting-loop/reports.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: Skill install or update. Verification: report with verdict. Memory: loops/skill-vetting-loop/reports.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
