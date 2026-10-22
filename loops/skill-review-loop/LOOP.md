---
name: skill-review
title: Skill Review skill
repo: sanyuan0704/sanyuan-skills
license: MIT
url: https://gethabit.dev/skills/sanyuan0704/skill-review
---

# Skill Review skill

The skill review skill helps skill authors audit Claude Code skills for structure, description quality, workflow design, token efficiency and anti-patterns, with specific fixes.

- Install the skill: `npx skills add sanyuan0704/sanyuan-skills --skill skill-review`
- Source: https://github.com/sanyuan0704/sanyuan-skills/tree/HEAD/skills/skill-review
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You want to review a skill; You lint a SKILL.md; You improve a skill's description.
Skip it when: You review application code; You need to write a skill from scratch.

# Make it a habit: Every skill change gets reviewed.

When a SKILL.md changes, your agent loads the skill, checks structure, description, workflow, token efficiency and anti-patterns, and reports strengths and prioritized fixes. A log keeps past reviews per skill so repeat issues show.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** SKILL.md changed (event; GitHub Actions or Claude Code routine; `pull_request touches **/SKILL.md`)
- **Verification:** structure checks pass. Hard checks: SKILL.md is under 500 lines; frontmatter holds only allowed keys; no TODO, FIXME, xxx or TBD left; report lists at least 2 strengths and each suggestion has What, Where and Fix. On fail: notify, max 0 retries.
- **Memory:** skill reviews log at `loops/skill-review-loop/run-log.md`. Read first: earlier suggestions for the same skill.

## Steps

1. **Load target.** Read the full SKILL.md, list all files and count its lines.
2. **Analyze.** Check the five dimensions with references/review-criteria.md.
3. **Find anti-patterns.** Look for vague directives, placeholders and a missing pre-delivery checklist.
4. **Report.** Write strengths with quotes, then suggestions sorted by impact.

Stop rule: Stops after one skill per run.

## Permissions

- Writes: loops/skill-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/skill-review-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: SKILL.md changed. Verification: structure checks pass. Memory: loops/skill-review-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
