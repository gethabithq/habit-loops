---
name: golang-pro
title: Golang Pro skill
repo: Jeffallan/claude-skills
license: MIT
url: https://gethabit.dev/skills/jeffallan/golang-pro
---

# Golang Pro skill

The golang pro skill helps agents write idiomatic Go: concurrency with goroutines and channels, gRPC or REST microservices, generics, error handling, pprof profiling and table-driven tests. For Go developers building production systems.

- Install the skill: `npx skills add Jeffallan/claude-skills --skill golang-pro`
- Source: https://github.com/Jeffallan/claude-skills/tree/HEAD/skills/golang-pro
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You build concurrent Go services; You write table-driven tests and benchmarks; You design gRPC microservices in Go.
Skip it when: Your project is not in Go; You need only a quick script.

# Make it a habit: Go changes that pass every gate.

When a pull request changes Go code, your agent runs go vet, golangci-lint and the tests with the race detector, checks coverage and the skill's must-do rules, and fixes what fails. A run log keeps the issues found for the next run.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR changes Go files (event; GitHub Actions or Claude Code routine; `pull_request paths: **/*.go`)
- **Verification:** vet, lint, race clean. Hard checks: go vet ./... passes; golangci-lint run reports no issues; tests pass with the -race flag; coverage is 80% or more; gofmt leaves no changes. On fail: retry, max 2 retries.
- **Memory:** lint and race log at `loops/go-quality-gate-loop/run-log.md`. Read first: lint issues and race findings from earlier runs.

## Steps

1. **Read the log.** The agent reads which issues came up in earlier runs.
2. **Review the design.** It checks module structure, small interfaces and goroutine lifecycles with the matching reference file.
3. **Check the rules.** It checks context on blocking calls, explicit error handling with %w and docs on exported names.
4. **Vet and lint.** It runs go vet ./... and golangci-lint run and fixes every issue.
5. **Test with race.** It runs table-driven tests with -race and checks coverage.
6. **Write the log.** It records fixes and open points in the run log.

Stop rule: Stops after one pull request and at most 2 fix retries.

## Permissions

- Writes: **/*.go, loops/go-quality-gate-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/go-quality-gate-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR changes Go files. Verification: vet, lint, race clean. Memory: loops/go-quality-gate-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
