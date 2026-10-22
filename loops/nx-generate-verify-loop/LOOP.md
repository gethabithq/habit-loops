---
name: nx-generate
title: Run Nx Generator skill
repo: nrwl/nx-ai-agents-config
license: MIT
url: https://gethabit.dev/skills/nrwl/nx-generate
---

# Run Nx Generator skill

Run Nx Generator (the nx-generate skill) scaffolds libraries, apps and features in an Nx monorepo: it finds the right generator, reads its source, dry-runs, generates and verifies with build, lint, test and typecheck. For developers working in an Nx workspace.

- Install the skill: `npx skills add nrwl/nx-ai-agents-config --skill nx-generate`
- Source: https://github.com/nrwl/nx-ai-agents-config/tree/HEAD/artifacts/skills/nx-generate
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: creating a new library or app in Nx; running a workspace or plugin generator; scaffolding boilerplate consistently.
Skip it when: the repo is not an Nx monorepo; no suitable generator exists.

# Make it a habit: Scaffolded code that passes checks.

When you need a new library or app, your agent finds the right Nx generator, reads its source, dry-runs it, generates, formats, then runs build, lint, test and typecheck. A run log keeps which generators and options were used.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** you ask to scaffold (manual; Claude Code routine; `run nx-generate on demand`)
- **Verification:** format and target checks. Hard checks: dry-run shows files in the expected location; nx format --fix leaves no unformatted files; nx run-many build, lint, test and typecheck pass. On fail: retry, max 2 retries.
- **Memory:** generator usage log at `loops/nx-generate-verify-loop/run-log.md`. Read first: the generators and options used before and the repo's critical targets.

## Steps

1. **Discover.** Your agent lists generators with npx nx list to find what the workspace offers.
2. **Match.** It picks the generator for your request, preferring a local workspace generator over an external one.
3. **Read options and source.** It reads the --help options and the generator source to learn exactly what it creates.
4. **Study patterns.** It looks at similar existing projects for naming, structure and tooling.
5. **Dry-run.** It runs the generator with --dry-run --no-interactive to check file placement.
6. **Generate.** It runs the generator with --no-interactive and adjusts the generated code if needed.
7. **Format and verify.** It runs nx format --fix, then build, lint, test and typecheck across affected projects.

Stop rule: Stops after one generator run per request, with at most 2 fix retries before escalating to you.

## Permissions

- Writes: libs/**, apps/**, tools/**, loops/nx-generate-verify-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/nx-generate-verify-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: you ask to scaffold. Verification: format and target checks. Memory: loops/nx-generate-verify-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
