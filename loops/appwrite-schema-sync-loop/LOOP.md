---
name: appwrite-cli
title: Appwrite CLI skill
repo: appwrite/skills
license: BSD-3-Clause
url: https://gethabit.dev/skills/appwrite/appwrite-cli
---

# Appwrite CLI skill

Appwrite cli is a skill for developers who use the Appwrite CLI well: config vs client, pull and push, type-safe code with appwrite generate, query flags, CI auth, regional endpoints and function variables.

- Install the skill: `npx skills add appwrite/skills --skill appwrite-cli`
- Source: https://github.com/appwrite/skills/tree/HEAD/skills/appwrite-cli
- Licence: BSD-3-Clause (Habit links to this skill and does not host or change it)

Use it when: You deploy Appwrite functions; You generate types from a table schema; You set up Appwrite in CI.
Skip it when: You need a full command list; You do not use Appwrite.

# Make it a habit: Schema, config and types stay synced.

When appwrite.config.json changes, your agent reviews the change table, pushes only the changed resource, reruns appwrite generate and runs the type checker. Secrets stay in the environment, never in the config.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** config file changes (event; GitHub Actions or Claude Code routine; `push touching appwrite.config.json`)
- **Verification:** push and type check. Hard checks: the change table shows no remote value against an empty local column; appwrite generate finishes; the project's type checker passes; appwrite.config.json holds no API key. On fail: stop, max 0 retries.
- **Memory:** config commit history at `appwrite.config.json`. Read first: the last pushed config and generated output path.

## Steps

1. **Read the config.** Read appwrite.config.json and confirm the regional endpoint and project.
2. **Check the change table.** If local is empty where remote has values, run appwrite pull for that resource first.
3. **Ask before force.** Ask the user, then push the one changed resource with --force instead of push all.
4. **Keep variables.** Push functions without --with-variables unless the user means to sync secrets.
5. **Regenerate types.** Run appwrite generate, or appwrite types for other languages, with the repo's usual output path.
6. **Type check.** Run the project's formatter and type checker on the generated code.

Stop rule: Stops after one resource push per run; no retries.

## Permissions

- Writes: appwrite.config.json, generated/**
- Network: cloud.appwrite.io, fra.cloud.appwrite.io
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`appwrite.config.json`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: config file changes. Verification: push and type check. Memory: appwrite.config.json. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
