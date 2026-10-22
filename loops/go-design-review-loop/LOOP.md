---
name: golang-design-patterns
title: Golang Design Patterns skill
repo: samber/cc-skills-golang
license: MIT
url: https://gethabit.dev/skills/samber/golang-design-patterns
---

# Golang Design Patterns skill

The golang design patterns skill guides agents to idiomatic Go: functional options, no init() or global state, safe enums, timeouts, retries, streaming and a fitting architecture. For Go developers who design APIs or review structure.

- Install the skill: `npx skills add samber/cc-skills-golang --skill golang-design-patterns`
- Source: https://github.com/samber/cc-skills-golang/tree/HEAD/skills/golang-design-patterns
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You design a new Go package or API; You set up graceful shutdown or retries; You review Go code for design issues.
Skip it when: You need a DI container comparison; You only fix error wrapping.

# Make it a habit: Go code stays idiomatic and bounded.

Each week your agent runs golang design patterns in review mode over the Go code: it looks for init() misuse, unbounded resources, missing timeouts and hidden global state. It reports before it refactors, and keeps a board of open design issues.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly design review (schedule; Claude Code routine or cron; `0 8 * * 1`)
- **Verification:** tests pass, you choose. Hard checks: go build ./... passes; go test ./... passes; count of init() functions does not grow. On fail: notify, max 0 retries.
- **Memory:** design issues board at `loops/go-design-review-loop/board.md`. Read first: open design issues and the agreed architecture style.

## Steps

1. **Read the board.** Load open issues and the architecture the developer chose last time.
2. **Scan the code.** Look for init() misuse, mutable globals, unbounded pools and external calls without a timeout.
3. **Check the idioms.** Compare against the best practices list, such as functional options and enums that start at 1.
4. **Report first.** List findings before any refactor is suggested.
5. **Ask on architecture.** Ask the developer which architecture they prefer before proposing clean, hexagonal, DDD or flat layout.
6. **Hand off details.** Send error handling, context and interface questions to the matching samber golang skills.

Stop rule: Stops after ten findings per run.

## Permissions

- Writes: loops/go-design-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/go-design-review-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly design review. Verification: tests pass, you choose. Memory: loops/go-design-review-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
