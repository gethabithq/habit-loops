---
name: golang-error-handling
title: Golang Error Handling skill
repo: samber/cc-skills-golang
license: MIT
url: https://gethabit.dev/skills/samber/golang-error-handling
---

# Golang Error Handling skill

The golang error handling skill teaches Go developers idiomatic error handling: wrapping with %w, errors.Is and errors.As, errors.Join, sentinel and custom errors, panic and recover, and structured logging with slog.

- Install the skill: `npx skills add samber/cc-skills-golang --skill golang-error-handling`
- Source: https://github.com/samber/cc-skills-golang/tree/HEAD/skills/golang-error-handling
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You write or review Go error handling; Your logs show duplicate errors; You add structured logging with slog.
Skip it when: You need the full samber/oops API; Your project is not Go.

# Make it a habit: No swallowed or double-logged errors.

When a pull request changes Go code, your agent reviews its error handling with golang-error-handling: unchecked errors, missing %w context, log-and-return pairs, panic misuse and non-slog logging. golangci-lint and the tests must pass, and a log keeps findings.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR changes Go files (event; GitHub Actions or Claude Code routine; `pull_request paths: **/*.go`)
- **Verification:** lint, tests, error rules. Hard checks: golangci-lint passes; tests pass; no returned error is discarded with _ in the diff; no error is both logged and returned in the same function; error strings in the diff start lowercase with no trailing punctuation. On fail: notify, max 0 retries.
- **Memory:** error findings log at `loops/go-error-handling-review-loop/runs.md`. Read first: packages with repeat error handling findings.

## Steps

1. **Read the diff.** The agent lists changed Go functions that create, wrap, log or return errors.
2. **Check creation.** It checks errors.New and fmt.Errorf use, lowercase messages and sentinel versus custom types.
3. **Check wrapping.** It checks %w inside the code, %v at system boundaries, and errors.Is or errors.As for inspection.
4. **Check single handling.** It finds log-and-return pairs, swallowed errors and errors discarded with _.
5. **Check panic and logging.** It flags panic for expected cases and logging without slog.
6. **Run lint and tests.** It runs golangci-lint and the tests, comments findings and logs them.

Stop rule: Stops after one pull request per run.

## Permissions

- Writes: loops/go-error-handling-review-loop/**
- Network: api.github.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/go-error-handling-review-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR changes Go files. Verification: lint, tests, error rules. Memory: loops/go-error-handling-review-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
