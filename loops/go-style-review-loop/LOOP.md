---
name: golang-code-style
title: Golang Code Style skill
repo: samber/cc-skills-golang
license: MIT
url: https://gethabit.dev/skills/samber/golang-code-style
---

# Golang Code Style skill

The golang code style skill gives Go developers clear style rules that linters cannot judge: line breaking, variable declarations, control flow, function design, comments and file layout. Use it when writing or reviewing Go code.

- Install the skill: `npx skills add samber/cc-skills-golang --skill golang-code-style`
- Source: https://github.com/samber/cc-skills-golang/tree/HEAD/skills/golang-code-style
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You review Go code for clarity; You set coding standards for a Go team; You clean up deep nesting or long signatures.
Skip it when: You need naming rules; You need linter configuration.

# Make it a habit: Go code stays clear, not clever.

When a pull request changes .go files, your agent reviews them with golang-code-style: early returns, no needless else, named booleans, field names in literals, initialized slices and maps. golangci-lint and the tests must pass. A log keeps repeat issues.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR changes Go files (event; GitHub Actions or Claude Code routine; `pull_request paths: **/*.go`)
- **Verification:** lint and tests pass. Hard checks: golangci-lint passes; tests pass; no line in the diff is longer than about 120 characters; calls with 4 or more arguments use one argument per line. On fail: notify, max 0 retries.
- **Memory:** style findings log at `loops/go-style-review-loop/runs.md`. Read first: style rules broken most often in past reviews.

## Steps

1. **Read the diff.** The agent lists changed Go files and functions in the pull request.
2. **Split by concern.** On a large diff it uses up to 5 sub-agents, one per style concern.
3. **Check control flow.** It looks for deep nesting, else after return, and conditions with 3 or more operands.
4. **Check declarations.** It checks := versus var, nil slices and maps, and composite literals without field names.
5. **Check functions.** It flags more than 4 parameters, context not first and naked returns in long functions.
6. **Run linters and tests.** It runs golangci-lint and the tests, then comments findings and logs them.

Stop rule: Stops after one pull request per run.

## Permissions

- Writes: loops/go-style-review-loop/**
- Network: api.github.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/go-style-review-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR changes Go files. Verification: lint and tests pass. Memory: loops/go-style-review-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
