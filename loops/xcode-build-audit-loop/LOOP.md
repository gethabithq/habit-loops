---
name: xcode-build-orchestrator
title: Xcode Build Orchestrator skill
repo: avdlee/xcode-build-optimization-agent-skill
license: MIT
url: https://gethabit.dev/skills/avdlee/xcode-build-orchestrator
---

# Xcode Build Orchestrator skill

Xcode Build Orchestrator runs an end-to-end Xcode build speed-up: benchmark, specialist analysis, ranked recommendations, an approval gate and re-benchmarking, delegating fixes to xcode-build-fixer. For iOS developers auditing slow builds.

- Install the skill: `npx skills add avdlee/xcode-build-optimization-agent-skill --skill xcode-build-orchestrator`
- Source: https://github.com/avdlee/xcode-build-optimization-agent-skill/tree/HEAD/skills/xcode-build-orchestrator
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: running a full Xcode build audit; finding what makes builds slow; wanting a recommend-first optimization pass.
Skip it when: you already have an approved plan to apply; the project is not an Xcode project.

# Make it a habit: A ranked, approved build speed-up plan.

On demand, your agent benchmarks the Xcode build, runs the specialist analyzers, ranks findings by likely wall-clock saving, and writes a plan for your approval, then hands approved items to the fixer. The plan in .build-benchmark/ is the memory.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** You request a build audit (manual; Claude Code routine; `run xcode-build-orchestrator on demand`)
- **Verification:** baseline and plan written. Hard checks: the benchmark artifact has non-empty timing_summary_categories; optimization-plan.md is written with an approval checklist; high-variance benchmarks are flagged when the spread exceeds 20% of the median. On fail: notify, max 0 retries.
- **Memory:** optimization plan at `.build-benchmark/optimization-plan.md`. Read first: the latest baseline benchmark and prior recommendations.

## Steps

1. **Collect context.** Your agent gathers the workspace or project, scheme, configuration, destination and the main pain point.
2. **Benchmark.** It runs the benchmark to establish a baseline, including cached clean builds when caching is on.
3. **Check confidence.** It flags high variance when the min-to-max spread exceeds 20% of the median.
4. **Run analyzers.** It applies the compilation, project and SPM analyzers that fit the evidence.
5. **Rank.** It merges findings and ranks them by likely wall-clock saving, not cumulative task time.
6. **Write plan.** It generates optimization-plan.md with impact language and an approval checklist, then stops.
7. **Hand off.** After you check the boxes it delegates the approved items to xcode-build-fixer and re-benchmarks.

Stop rule: Stops after one analyze-and-plan pass per run; it never changes files before your approval.

## Permissions

- Writes: .build-benchmark/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`.build-benchmark/optimization-plan.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: You request a build audit. Verification: baseline and plan written. Memory: .build-benchmark/optimization-plan.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
