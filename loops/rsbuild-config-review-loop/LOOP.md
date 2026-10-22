---
name: rsbuild-best-practices
title: Rsbuild Best Practices skill
repo: rstackjs/agent-skills
license: MIT
url: https://gethabit.dev/skills/rstackjs/rsbuild-best-practices
---

# Rsbuild Best Practices skill

The rsbuild best practices skill helps developers configure, review and troubleshoot Rsbuild apps: config layout, CLI commands, type checking, bundle size, assets, source map safety, debugging and profiling.

- Install the skill: `npx skills add rstackjs/agent-skills --skill rsbuild-best-practices`
- Source: https://github.com/rstackjs/agent-skills/tree/HEAD/skills/rsbuild-best-practices
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: setting up an Rsbuild project; reviewing an Rsbuild config change; a build is slow or too large.
Skip it when: you use a different bundler; you need Rspack internals only.

# Make it a habit: Rsbuild builds stay lean and safe.

When a pull request changes your Rsbuild config or dependencies, your agent reviews it against the Rsbuild best practices, runs rsbuild build and a type check, and logs findings so later reviews know which rules keep slipping.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR changes build config (event; GitHub Actions or Claude Code routine; `pull_request.opened or synchronize, rsbuild.config.ts or package files`)
- **Verification:** build and type check. Hard checks: rsbuild build passes; tsc --noEmit passes; no .map files in published output when source maps are on; config uses defineConfig in rsbuild.config.ts. On fail: notify, max 1 retries.
- **Memory:** Rsbuild review log at `loops/rsbuild-config-review-loop/log.md`. Read first: rule breaks found in earlier reviews.

## Steps

1. **Read the diff.** The agent checks changes to rsbuild.config.ts, tsconfig.json and dependencies.
2. **Check configuration rules.** It flags tools.rspack or tools.bundlerChain where a first-class option exists, and missing source.entry for multi-page apps.
3. **Check bundle habits.** Heavy imports on non-critical paths get a suggestion to use dynamic import().
4. **Check assets.** Source assets should come from source folders, and public files by absolute URL path.
5. **Build and type check.** It runs rsbuild build and tsc --noEmit, and reads dist/.rsbuild to confirm the final config.
6. **Report and log.** Findings go into a review comment and the log.

Stop rule: Stops after one pull request and at most 2 build reruns.

## Permissions

- Writes: loops/rsbuild-config-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/rsbuild-config-review-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR changes build config. Verification: build and type check. Memory: loops/rsbuild-config-review-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
