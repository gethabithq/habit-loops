---
name: neon-postgres-branches
title: Neon Postgres Branches skill
repo: neondatabase/agent-skills
license: Apache-2.0
url: https://gethabit.dev/skills/neondatabase/neon-postgres-branches
---

# Neon Postgres Branches skill

The neon postgres branches skill helps developers pick and create the right Neon branch, normal or schema-only, reset branches from parent and set branch lifecycles for CI and pull requests.

- Install the skill: `npx skills add neondatabase/agent-skills --skill neon-postgres-branches`
- Source: https://github.com/neondatabase/agent-skills/tree/HEAD/plugins/neon-postgres/skills/neon-postgres-branches
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You test risky migrations on real data; Production data is sensitive; You want a database branch per pull request.
Skip it when: Your database is not on Neon; You need point-in-time recovery.

# Make it a habit: Each PR gets its own database.

When a pull request opens, your agent picks a normal or schema-only Neon branch, creates it with an expiry using the Neon CLI and validates it. It asks before touching your .env, and logs each branch so the run on close can clean it up.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** pull request opened (event; GitHub Actions or Claude Code routine; `pull_request.opened, pull_request.closed`)
- **Verification:** branch exists + your OK. Hard checks: neon --version and neon projects list succeed; neon branches create returns the new branch; branch has --expires-at set; describe_branch or neon connection-string finds the branch. On fail: notify, max 1 retries.
- **Memory:** branches per PR at `loops/neon-branch-per-pr-loop/run-log.md`. Read first: open branches, their PR and expiry time.

## Steps

1. **Load parent skill.** The agent uses the parent neon skill first for the Neon overview.
2. **Choose type.** Normal branch for real-data migration tests, schema-only branch when data is sensitive; it asks if unclear.
3. **Check the CLI.** Run neon --version and neon projects list, and fall back to Neon MCP only if the CLI cannot be used.
4. **Create branch.** Run neon branches create with --name, --parent and --expires-at, plus --schema-only when needed.
5. **Validate.** Fetch the branch with neon connection-string or describe_branch.
6. **Ask about .env.** Ask before writing the new DATABASE_URL and never overwrite a key without your yes.
7. **Clean up.** On PR close, delete the branch listed in the run log.

Stop rule: One branch per pull request per run, one retry on create.

## Permissions

- Writes: .env, loops/neon-branch-per-pr-loop/**
- Network: neon.com, console.neon.tech
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/neon-branch-per-pr-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: pull request opened. Verification: branch exists + your OK. Memory: loops/neon-branch-per-pr-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
