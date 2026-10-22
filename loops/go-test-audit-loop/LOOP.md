---
name: golang-testing
title: Golang Testing skill
repo: samber/cc-skills-golang
license: MIT
url: https://gethabit.dev/skills/samber/golang-testing
---

# Golang Testing skill

The golang testing skill helps Go developers write and review production-ready tests: table-driven tests, testify, parallel tests, fuzzing, goleak leak checks, synctest, coverage and integration tests with build tags.

- Install the skill: `npx skills add samber/cc-skills-golang --skill golang-testing`
- Source: https://github.com/samber/cc-skills-golang/tree/HEAD/skills/golang-testing
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You write tests for Go code; You audit a Go test suite for gaps; A Go test is flaky or slow.
Skip it when: You need benchmark methods; Your project is not Go.

# Make it a habit: Go tests stay fast, isolated, leak-free.

Each week your agent audits the Go test suite with golang-testing in audit mode: unit quality and coverage gaps, integration isolation, and goroutine leaks and races. go test -race must pass. It writes a gap report and keeps last week's to compare.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly test audit (schedule; Claude Code routine or GitHub Actions; `0 6 * * 3`)
- **Verification:** race-free tests pass. Hard checks: go test -race ./... passes; go test -tags=integration ./... passes; every table-driven case has a name passed to t.Run; integration tests carry the //go:build integration tag. On fail: notify, max 1 retries.
- **Memory:** weekly gap reports at `loops/go-test-audit-loop/reports.md`. Read first: last week's gaps and which were closed.

## Steps

1. **Read last report.** The agent opens last week's gap report.
2. **Audit unit tests.** One sub-agent checks unit test quality and finds gaps with go test -coverprofile=coverage.out ./....
3. **Audit integration tests.** A second sub-agent checks build tags and isolation of integration tests.
4. **Audit goroutines.** A third sub-agent checks goroutine leaks with goleak and race conditions.
5. **Run the suite.** It runs go test -race ./... and the integration tests.
6. **Write gap report.** It merges the findings into one gap report and marks new and closed gaps.

Stop rule: Stops after one audit with at most 20 gaps reported per run.

## Permissions

- Writes: loops/go-test-audit-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/go-test-audit-loop/reports.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly test audit. Verification: race-free tests pass. Memory: loops/go-test-audit-loop/reports.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
