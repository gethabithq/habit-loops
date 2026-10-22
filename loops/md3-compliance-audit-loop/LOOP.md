---
name: material-3
title: Material 3 skill
repo: hamen/material-3-skill
license: MIT
url: https://gethabit.dev/skills/hamen/material-3
---

# Material 3 skill

The material 3 skill implements Google's Material Design 3: Jetpack Compose Material3 first, plus Flutter and limited web, covering tokens, components, adaptive layout, theming, M3 Expressive and a compliance audit. For app developers using Material You.

- Install the skill: `npx skills add hamen/material-3-skill --skill material-3`
- Source: https://github.com/hamen/material-3-skill/tree/HEAD/skills/material-3
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: building a Material 3 UI in Compose; theming with dynamic color and tokens; auditing an app for MD3 compliance.
Skip it when: you use a different design system; you need M3 Expressive on the web.

# Make it a habit: Your UI stays Material 3 compliant.

When UI code changes, your agent runs the material-3 audit: it scores color, type, shape, elevation, components, layout, navigation, motion, accessibility and theming 0-10 and lists fixes. A run log keeps the scores per run.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** UI code changes (event; GitHub Actions or Claude Code routine; `pull request touching UI files`)
- **Verification:** audit score and greps. Hard checks: no hardcoded hex colors in CSS or SCSS; no @material/mdc- MD2 imports next to @material/web; no raw Color(0x...) for Compose surfaces without reason. Critic: claude-opus-5-5, pass at 70/100. On fail: notify, max 0 retries.
- **Memory:** audit score log at `loops/md3-compliance-audit-loop/run-log.md`. Read first: last audit's category scores and open critical issues.

## Steps

1. **Pick target.** Your agent takes the changed files or a running page as the audit target.
2. **Run quick checks.** It greps for hardcoded colors, raw Compose colors and MD2 imports.
3. **Score categories.** It scores the ten categories from 0 to 10 using the scoring guide.
4. **Write report.** It writes the MD3 Compliance Audit Report with critical issues, warnings and passing items.
5. **Prioritize fixes.** It lists recommended fixes, most impactful first, with file and line references.

Stop rule: Stops after one audit report per change set; no retries.

## Permissions

- Writes: loops/md3-compliance-audit-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/md3-compliance-audit-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: UI code changes. Verification: audit score and greps. Memory: loops/md3-compliance-audit-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
