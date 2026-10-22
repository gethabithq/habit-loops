---
name: run-tests
title: .NET Run Tests skill
repo: dotnet/skills
license: MIT
url: https://gethabit.dev/skills/dotnet/run-tests
---

# .NET Run Tests skill

.NET Run Tests picks and runs the right dotnet test command for classic, VSTest, bridged MTP or native MTP projects, with correct filters for MSTest, xUnit, NUnit and TUnit plus TRX, dumps and coverage. For .NET developers.

- Install the skill: `npx skills add dotnet/skills --skill run-tests`
- Source: https://github.com/dotnet/skills/tree/HEAD/plugins/dotnet-test/skills/run-tests
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You run .NET tests; You need an exact dotnet test filter; You want TRX or coverage output.
Skip it when: You write test code; You set up hot reload loops.

# Make it a habit: Run the right dotnet test command.

On each pull request, your agent reads the repository overlay if present, works out classic, VSTest, bridged MTP or native MTP mode from global.json and project props, runs the smallest matching test command with correct filters and reports a literal Passed, Failed, Skipped summary.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** .NET pull request opened (event; GitHub Actions or Claude Code routine; `pull request touches .cs or .csproj files`)
- **Verification:** tests pass, scope matches. Hard checks: test run reports Failed: 0; reported test names or count match the requested filter; dotnet test options sit before any -- bridge separator; --project appears only in SDK 10+ native MTP mode. On fail: retry, max 1 retries.
- **Memory:** test command log at `loops/dotnet-test-run-loop/runs.md`. Read first: the detected mode and command that worked last time.

## Steps

1. **Read the overlay.** Your agent checks .agents/skill-overlays/dotnet-test/run-tests.md and applies it if its frontmatter matches.
2. **Read config.** It reads global.json, the project, packages.config and Directory.Build.props in one batch.
3. **Pick the mode.** It decides classic, VSTest, VSTest-to-MTP bridge or native MTP.
4. **Build the command.** It picks dotnet test syntax and the framework-correct filter for the scope.
5. **Add outputs.** It adds TRX, diagnostics, dumps or coverage flags that match the platform.
6. **Run and report.** It runs the command and reports command, exit code and the Passed, Failed, Skipped summary.

Stop rule: Stops after one test command and one filter fix rerun per run.

## Permissions

- Writes: loops/dotnet-test-run-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/dotnet-test-run-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: .NET pull request opened. Verification: tests pass, scope matches. Memory: loops/dotnet-test-run-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
