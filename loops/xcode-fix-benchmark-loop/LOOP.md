---
name: xcode-build-fixer
title: Xcode Build Fixer skill
repo: avdlee/xcode-build-optimization-agent-skill
license: MIT
url: https://gethabit.dev/skills/avdlee/xcode-build-fixer
---

# Xcode Build Fixer skill

Xcode Build Fixer applies approved Xcode build optimizations, build settings, script phase guards, source fixes and SPM restructuring, then re-benchmarks to prove the gain. For iOS developers acting on an optimization plan.

- Install the skill: `npx skills add avdlee/xcode-build-optimization-agent-skill --skill xcode-build-fixer`
- Source: https://github.com/avdlee/xcode-build-optimization-agent-skill/tree/HEAD/skills/xcode-build-fixer
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: applying an approved build optimization plan; implementing specific Xcode build fixes; verifying a fix with a benchmark.
Skip it when: you have no approved plan yet; the project is not an Xcode project.

# Make it a habit: Approved build fixes proven by benchmark.

When you approve a build optimization plan, your agent applies one fix at a time, confirms it compiles, re-benchmarks against the baseline and reports the wall-clock delta. The optimization plan is the memory it reads first.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** plan approved (event; Claude Code routine; `approval boxes checked in optimization-plan.md`)
- **Verification:** compiles and re-benchmarked. Hard checks: each change compiles with xcodebuild build; benchmark_builds.py reruns against the baseline inputs; post-change medians are compared and deltas reported. On fail: notify, max 1 retries.
- **Memory:** optimization plan at `.build-benchmark/optimization-plan.md`. Read first: the approval checklist and the baseline medians.

## Steps

1. **Read approvals.** Your agent reads the plan or your instruction and implements only the checked items.
2. **Apply one fix.** It applies one logical change, a build setting, script phase, source fix or SPM change, at a time.
3. **Verify compile.** It runs a quick xcodebuild build to confirm no errors were introduced.
4. **Re-benchmark.** After all approved changes it reruns benchmark_builds.py with the original baseline inputs.
5. **Compare.** It compares post-change medians to the baseline for clean, cached clean and incremental builds.
6. **Report.** It leads with the wall-clock result, lists files changed and flags any regression.

Stop rule: Stops after one approved plan per run, with at most one re-benchmark retry.

## Permissions

- Writes: project.pbxproj, source files, Package.swift, .build-benchmark/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`.build-benchmark/optimization-plan.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: plan approved. Verification: compiles and re-benchmarked. Memory: .build-benchmark/optimization-plan.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
