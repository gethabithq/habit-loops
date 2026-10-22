---
name: prisma-cli
title: Prisma CLI skill
repo: prisma/skills
license: MIT
url: https://gethabit.dev/skills/prisma/prisma-cli
---

# Prisma CLI skill

The prisma cli skill is a reference for the Prisma ORM 7 command line: init, generate, migrate, db, dev, studio and mcp, with a consent checkpoint before destructive commands. For developers on existing Prisma 7 apps.

- Install the skill: `npx skills add prisma/skills --skill prisma-cli`
- Source: https://github.com/prisma/skills/tree/HEAD/prisma-cli
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You run Prisma migrations; You regenerate Prisma Client; You use the local prisma dev database.
Skip it when: You work on Prisma 8; You need the Prisma Platform CLI.

# Make it a habit: Schema valid, migrations in sync.

When a pull request changes the Prisma 7 schema, your agent runs prisma validate, prisma format, prisma migrate status and prisma generate. Any destructive command waits for your explicit consent. The run log keeps the migration status per run.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** schema file changed (event; GitHub Actions or Claude Code routine; `pull_request touches prisma/schema.prisma or prisma/migrations`)
- **Verification:** validate + migrate status. Hard checks: prisma validate passes; prisma format leaves no diff; prisma migrate status shows no failed migration; prisma generate succeeds. On fail: notify, max 0 retries.
- **Memory:** migration status log at `loops/prisma-schema-check-loop/run-log.md`. Read first: last migration status and open schema problems.

## Steps

1. **Use project CLI.** The agent uses the project's version-matched prisma command, never a floating latest install.
2. **Validate.** It runs prisma validate and prisma format and checks for a diff.
3. **Check migrations.** It runs prisma migrate status, and prisma migrate dev --create-only when a new migration is needed.
4. **Generate client.** It runs prisma generate so the client matches the schema.
5. **Ask before data loss.** For migrate reset or db push --force-reset it reads references/agent-safety.md, explains the data loss and asks you first.
6. **Log.** It writes the status and results into the run log.

Stop rule: Stops after one schema change per run; no destructive command without fresh consent.

## Permissions

- Writes: prisma/migrations/**, the generated client folder, loops/prisma-schema-check-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/prisma-schema-check-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: schema file changed. Verification: validate + migrate status. Memory: loops/prisma-schema-check-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
