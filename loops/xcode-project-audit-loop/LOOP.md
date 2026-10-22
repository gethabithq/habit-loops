---
name: xcode-project-analyzer
title: Xcode Project Analyzer skill
repo: avdlee/xcode-build-optimization-agent-skill
license: MIT
url: https://gethabit.dev/skills/avdlee/xcode-project-analyzer
---

# Xcode Project Analyzer skill

The Xcode Project Analyzer skill (xcode-project-analyzer) audits Xcode project configuration, build settings, scheme order and script phases to find build-time wins, recommendation-first with approval gates. For iOS developers with slow builds.

- Install the skill: `npx skills add avdlee/xcode-build-optimization-agent-skill --skill xcode-project-analyzer`
- Source: https://github.com/avdlee/xcode-build-optimization-agent-skill/tree/HEAD/skills/xcode-project-analyzer
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: auditing Xcode project configuration; diagnosing slow incremental builds; reviewing schemes and script phases.
Skip it when: the slowness is clearly in source code; the project is not an Xcode project.

# Make it a habit: Project-level build waste found and ranked.

On demand, your agent audits the Xcode project: scheme order, target dependencies, build settings, script phases and module settings, each finding backed by evidence with an approval requirement. A run log keeps prior findings.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** you ask for project audit (manual; Claude Code routine; `run xcode-project-analyzer on demand`)
- **Verification:** findings backed by evidence. Hard checks: the Debug and Release build settings are compared against the recommended checklist; each finding names evidence and its likely scope; each finding states its approval requirement. On fail: notify, max 0 retries.
- **Memory:** project audit log at `loops/xcode-project-audit-loop/run-log.md`. Read first: prior findings and the build settings checklist results.

## Steps

1. **Review schemes.** Your agent reviews scheme build order and target dependencies for serial bottlenecks.
2. **Audit build settings.** It compares Debug and Release settings against the recommended checklist with checkmarks.
3. **Check script phases.** It checks run scripts for declared inputs and outputs and dependency analysis.
4. **Check modules.** It checks DEFINES_MODULE and explicit module dependency settings for module-map readiness.
5. **Inspect timing.** It looks at planning, asset catalog and zero-change build overhead in the timing summary.
6. **Report.** It records each finding with evidence, scope, impact and its approval requirement.

Stop rule: Stops after one project audit per run; it recommends and never changes project files.

## Permissions

- Writes: loops/xcode-project-audit-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/xcode-project-audit-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: you ask for project audit. Verification: findings backed by evidence. Memory: loops/xcode-project-audit-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
