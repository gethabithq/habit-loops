---
name: better-ui
title: Better UI skill
repo: jakubkrehel/skills
license: MIT
url: https://gethabit.dev/skills/jakubkrehel/better-ui
---

# Better UI skill

The better ui skill polishes surfaces, icons and motion with exact values for radius, shadows, press scale, transitions and icon states, and reports findings by severity. For frontend teams who care about UI detail.

- Install the skill: `npx skills add jakubkrehel/skills --skill better-ui`
- Source: https://github.com/jakubkrehel/skills/tree/HEAD/skills/better-ui
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You review UI pull requests; Motion or hover feels off; Icons and surfaces look uneven.
Skip it when: The interaction itself is broken; You need typography or color checks.

# Make it a habit: UI details stay exact and consistent.

On each pull request that touches UI code, your agent runs better ui: it checks radius, shadows, image outlines, press scale, motion and icons against the detection table and reports findings by severity. It ends with Block or Approve.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR touches UI code (event; GitHub Actions or Claude Code routine; `pull_request paths: **/*.css, **/*.tsx`)
- **Verification:** no HIGH findings left. Hard checks: no transition-all or will-change: all in the diff; no motion without a prefers-reduced-motion guard; count of HIGH findings is zero for Approve. On fail: notify, max 0 retries.
- **Memory:** polish findings log at `loops/ui-polish-review-loop/findings.md`. Read first: open findings and accepted project conventions.

## Steps

1. **Respect the project.** Keep its tokens and motion language, and treat a consistent choice as a preference.
2. **Scan surfaces.** Check nested radius, shadows versus borders and image outlines.
3. **Scan motion.** Check press scale, transitions, exits, stagger and reduced-motion gating.
4. **Scan icons.** Check stroke weight, currentColor and hover only on hover-capable pointers.
5. **Hand off.** Leave typography, accessibility, layout and colors to the sibling better skills.
6. **Report.** Write one row per root cause with severity and end with Block or Approve.

Stop rule: Stops after one pull request per run.

## Permissions

- Writes: loops/ui-polish-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/ui-polish-review-loop/findings.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR touches UI code. Verification: no HIGH findings left. Memory: loops/ui-polish-review-loop/findings.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
