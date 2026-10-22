---
name: r8-analyzer
title: R8 Analyzer skill
repo: android/skills
license: Apache-2.0
url: https://gethabit.dev/skills/android/r8-analyzer
---

# R8 Analyzer skill

R8 Analyzer analyses Android build files and R8 keep rules to find redundancies, overly broad rules and rules that subsume library consumer rules, reporting them to trim app size. For Android developers tuning Proguard and R8.

- Install the skill: `npx skills add android/skills --skill r8-analyzer`
- Source: https://github.com/android/skills/tree/HEAD/performance/r8-analyzer
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: optimizing app size; removing redundant or broad keep rules; troubleshooting Proguard config.
Skip it when: the project is not Android; you have no keep rules to review.

# Make it a habit: Leaner, non-redundant R8 keep rules.

On demand, your agent checks the build config, picks the analysis path by AGP and R8 version, and reports redundant, broad or subsuming keep rules in the strict report format. A run log keeps prior scores.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** you ask for R8 audit (manual; Claude Code routine; `run r8-analyzer on demand`)
- **Verification:** report in strict format. Hard checks: the AGP and R8 versions are read from the build files; the chosen path produces the analysis result file or manual findings; the output is only the Markdown report in the required format. On fail: notify, max 0 retries.
- **Memory:** keep rules log at `loops/r8-keep-rules-audit-loop/run-log.md`. Read first: prior scores and rule impact metrics.

## Steps

1. **Check config.** Your agent inspects the gradle build files and flags missing optimizations and full-mode settings.
2. **Pick path.** It selects Path A, B or C by the AGP and R8 versions.
3. **Generate data.** On Path A it runs the standalone gradle task, converts the report and runs the analysis script.
4. **Evaluate rules.** It finds redundant library rules, broad package-wide rules and subsuming rules.
5. **Report.** It outputs only the Markdown report in the strict format, with no extra text and no file changes.

Stop rule: Stops after one analysis per run; it suggests only and changes no files.

## Permissions

- Writes: tmp/keepradius/**, app/build/reports/r8/**, loops/r8-keep-rules-audit-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/r8-keep-rules-audit-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: you ask for R8 audit. Verification: report in strict format. Memory: loops/r8-keep-rules-audit-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
