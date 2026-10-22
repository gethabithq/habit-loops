---
name: supabase
title: Supabase skill
repo: supabase/agent-skills
license: MIT
url: https://gethabit.dev/skills/supabase/supabase
---

# Supabase skill

The supabase skill guides an agent through any Supabase task: database, auth, RLS, Edge Functions, storage, CLI and MCP, with a security checklist and a fixed way to make and commit schema changes. For developers who build on Supabase.

- Install the skill: `npx skills add supabase/agent-skills --skill supabase`
- Source: https://github.com/supabase/agent-skills/tree/HEAD/skills/supabase
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You change a Supabase schema; You write RLS policies; You debug a Supabase error.
Skip it when: You do not use Supabase; You only need plain Postgres help.

# Make it a habit: Safe schema changes, checked migrations.

When a pull request changes the Supabase schema, your agent checks the changelog for breaking changes, runs supabase db advisors, walks the security checklist, generates the migration and runs a test query. The run log keeps advisor findings.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** schema change in PR (event; GitHub Actions or Claude Code routine; `pull_request touching supabase/schemas or supabase/migrations`)
- **Verification:** advisors + test query. Hard checks: supabase db advisors reports no open issues; every table in an exposed schema has RLS enabled; supabase migration list --local shows the new migration; a test query confirms the change works. On fail: notify, max 2 retries.
- **Memory:** advisor findings log at `loops/supabase-schema-guard-loop/run-log.md`. Read first: past advisor findings and breaking changes already checked.

## Steps

1. **Check the changelog.** The agent fetches https://supabase.com/changelog.md and follows any breaking-change entry that fits the task.
2. **Pick the workflow.** It uses declarative schemas if supabase/schemas/ exists, otherwise imperative migrations with supabase migration new <name>.
3. **Run advisors.** It runs supabase db advisors, or MCP get_advisors on older CLI versions, and fixes issues.
4. **Walk the checklist.** It checks views, SECURITY DEFINER functions, RLS policies with USING and WITH CHECK, and storage grants.
5. **Generate the migration.** It runs supabase db pull <descriptive-name> --local --yes, then supabase migration list --local.
6. **Verify.** It runs a test query and stops to rethink after two or three failed attempts.

Stop rule: Stops after one schema change per run and at most three attempts per approach.

## Permissions

- Writes: supabase/migrations/**, supabase/schemas/**, loops/supabase-schema-guard-loop/**
- Network: supabase.com, mcp.supabase.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/supabase-schema-guard-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: schema change in PR. Verification: advisors + test query. Memory: loops/supabase-schema-guard-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
