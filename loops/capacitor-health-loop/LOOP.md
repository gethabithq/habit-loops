---
name: capacitor-best-practices
title: Capacitor Best Practices skill
repo: cap-go/capgo-skills
license: MIT
url: https://gethabit.dev/skills/cap-go/capacitor-best-practices
---

# Capacitor Best Practices skill

The capacitor best practices skill reviews and sets up Capacitor apps: version alignment, capacitor.config audit, plugin patterns, native project checks and release prep, with fixes for common errors. For mobile teams on Capacitor.

- Install the skill: `npx skills add cap-go/capgo-skills --skill capacitor-best-practices`
- Source: https://github.com/cap-go/capgo-skills/tree/HEAD/plugins/capacitor-core/skills/capacitor-best-practices
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: reviewing a Capacitor codebase; auditing capacitor.config.ts; fixing a plugin not implemented error.
Skip it when: you need a security audit; you plan a major version upgrade.

# Make it a habit: Capacitor app stays release ready.

Each week your agent reviews the Capacitor app with capacitor-best-practices: version drift, config, plugin patterns and native projects. It reports findings by severity, asks before invasive fixes, runs the skill's verification commands and keeps a findings board.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly app review (schedule; Claude Code routine or GitHub Actions; `0 8 * * 1`)
- **Verification:** skill verification commands pass. Hard checks: npm ls shows one version for all @capacitor core packages; npm run build && npx cap sync succeeds; no url, cleartext or webContentsDebuggingEnabled in synced native config; git status --porcelain on generated web assets is empty; no error.message comparisons in src/; ./gradlew assembleRelease and xcodebuild succeed. On fail: notify, max 0 retries.
- **Memory:** capacitor findings board at `loops/capacitor-health-loop/board.md`. Read first: open findings, their severity and which fixes you approved.

## Steps

1. **Take inventory.** Your agent runs npx cap doctor and npx cap ls, reads capacitor.config.ts and checks for SPM or CocoaPods.
2. **Review by area.** It works through config, versions, plugins, native iOS, native Android, live updates and release one at a time.
3. **Report findings.** It lists findings by severity with file:line and the fix before it edits anything.
4. **Ask first.** For a major upgrade, SPM migration, R8 or a new appId it asks you before changing anything.
5. **Fix with references.** It applies fixes using the matching file such as references/plugins.md or references/native-projects.md.
6. **Run verification.** It runs the version, sync, config, asset, error-handling and native build checks.
7. **Hand off deep topics.** Security, performance, tests and upgrades go to their sibling skills, such as capacitor-security.

Stop rule: Stops after five fixes per run; invasive changes wait for your yes.

## Permissions

- Writes: loops/capacitor-health-loop/**, src/**, capacitor.config.ts, android/**, ios/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/capacitor-health-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly app review. Verification: skill verification commands pass. Memory: loops/capacitor-health-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
