---
name: prisma-driver-adapter-implementation
title: Prisma Driver Adapter Implementation skill
repo: prisma/skills
license: MIT
url: https://gethabit.dev/skills/prisma/prisma-driver-adapter-implementation
---

# Prisma Driver Adapter Implementation skill

The prisma driver adapter implementation skill is a reference for building Prisma ORM 7 SQL driver adapters: transaction lifecycle, savepoints, result mapping, error preservation and a verification checklist. For developers who write or change database adapters.

- Install the skill: `npx skills add prisma/skills --skill prisma-driver-adapter-implementation`
- Source: https://github.com/prisma/skills/tree/HEAD/prisma-driver-adapter-implementation
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You build a new driver adapter; You debug P2039 errors; You add savepoint support.
Skip it when: You only write Prisma queries; You work on Prisma 8.

# Make it a habit: Driver adapter changes pass the checklist.

When a pull request changes a Prisma ORM 7 SQL driver adapter, your agent walks the skill's verification checklist: typecheck, result mapping, transactions, savepoints, error mapping and shadow database cleanup. Integration tests must pass. The run log keeps open items.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR touches adapter code (event; GitHub Actions or Claude Code routine; `pull_request touching SqlDriverAdapter or Transaction code`)
- **Verification:** typecheck + E2E tests. Hard checks: typecheck passes against the exact @prisma/driver-adapter-utils version; Prisma Client integration/E2E tests pass; nested transaction tests cover create, rollback and release savepoint; unmapped database errors keep originalCode and originalMessage. On fail: notify, max 1 retries.
- **Memory:** checklist status log at `loops/prisma-adapter-check-loop/run-log.md`. Read first: checklist items still open from earlier runs.

## Steps

1. **Match the version.** The agent pins the @prisma/driver-adapter-utils version of the target Prisma release and typechecks.
2. **Check queries.** It checks that queryRaw keeps column order, types, nulls and precision, and that executeRaw reports affected rows.
3. **Check transactions.** It checks one dedicated connection per transaction and that commit and rollback release it exactly once.
4. **Check errors.** It checks DriverAdapterError mapping and that unknown errors keep their original code and message.
5. **Check cleanup.** It checks dispose ownership and that the shadow database is isolated and always dropped.
6. **Run E2E tests.** It runs Prisma Client integration tests, not only adapter unit tests, and logs open items.

Stop rule: Stops after one pull request per run and one fix attempt.

## Permissions

- Writes: loops/prisma-adapter-check-loop/**
- Network: api.github.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/prisma-adapter-check-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR touches adapter code. Verification: typecheck + E2E tests. Memory: loops/prisma-adapter-check-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
