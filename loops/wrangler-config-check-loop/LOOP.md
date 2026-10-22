---
name: wrangler
title: Wrangler skill
repo: cloudflare/skills
license: Apache-2.0
url: https://gethabit.dev/skills/cloudflare/wrangler
---

# Wrangler skill

Wrangler is a skill that runs and troubleshoots Wrangler CLI commands in projects with a Wrangler config: local dev, Previews, deploys, secrets and resources, checked against current Cloudflare docs. For Workers developers.

- Install the skill: `npx skills add cloudflare/skills --skill wrangler`
- Source: https://github.com/cloudflare/skills/tree/HEAD/skills/wrangler
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: Your project has a wrangler.jsonc or wrangler.toml; You add a binding or environment; You set up Workers Previews.
Skip it when: You start a new project without Wrangler config; Your project uses cloudflare.config.ts.

# Make it a habit: Config changes checked before deploy.

When a pull request changes the Wrangler config, your agent checks the target environment and bindings against current docs, regenerates types with wrangler types, runs the typecheck and a wrangler deploy --dry-run. It reports what changed and any gaps. A run log keeps results.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** Wrangler config changed (event; GitHub Actions; `pull_request that changes wrangler.jsonc, wrangler.json or wrangler.toml`)
- **Verification:** types, typecheck, dry run. Hard checks: wrangler types runs and generated types are current; the project typecheck passes; wrangler deploy --dry-run succeeds for the intended environment; no secret value appears in config or command arguments. On fail: notify, max 1 retries.
- **Memory:** checks and gaps per PR at `loops/wrangler-config-check-loop/run-log.md`. Read first: open validation gaps from the last run.

## Steps

1. **Inspect the project.** Find the package manager, local Wrangler version, scripts and the config the build uses.
2. **Fix the target.** Name the account, Worker, environment and resource the change affects.
3. **Retrieve docs.** Check flags and fields in wrangler --help, the installed config-schema.json and Cloudflare docs.
4. **Check environments.** Confirm bindings and variables are set per environment where inheritance does not apply.
5. **Validate.** Run wrangler types, the typecheck and wrangler deploy --dry-run.
6. **Report.** Report what changed, the target, checks run and any gaps a dry run cannot prove.

Stop rule: Stops after one pull request per run, with at most 1 retry.

## Permissions

- Writes: loops/wrangler-config-check-loop/**
- Network: developers.cloudflare.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/wrangler-config-check-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: Wrangler config changed. Verification: types, typecheck, dry run. Memory: loops/wrangler-config-check-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
