---
name: astro-framework
title: Astro Framework skill
repo: delineas/astro-framework-agents
license: MIT
url: https://gethabit.dev/skills/delineas/astro-framework
---

# Astro Framework skill

The astro framework skill helps web developers build fast content sites with Astro islands: hydration directives, server islands, Content Layer loaders, SSR adapters, sessions, actions and i18n.

- Install the skill: `npx skills add delineas/astro-framework-agents --skill astro-framework`
- Source: https://github.com/delineas/astro-framework-agents/tree/HEAD/skills/astro-framework
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You build an Astro component; You choose a client directive; You set up content collections.
Skip it when: You build a full SPA; You use Next.js or SvelteKit.

# Make it a habit: Astro pages ship only needed JavaScript.

On every pull request to an Astro site, your agent checks client directives against the decision tree, flags hydrated components that need none, checks content collections use loaders and Zod in src/content.config.ts, and runs the build. A log keeps findings.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** Astro pull request (event; GitHub Actions or Claude Code routine; `pull_request touches .astro files or astro.config.mjs`)
- **Verification:** build and rules pass. Hard checks: the Astro build passes; no client:only without a framework; no new src/content/config.ts; collections use loaders in src/content.config.ts; no functions passed as props to server:defer components. On fail: notify, max 0 retries.
- **Memory:** hydration findings log at `loops/astro-hydration-review-loop/run-log.md`. Read first: components flagged before and the output mode in use.

## Steps

1. **List directives.** Collect client:* and server:defer uses in the change.
2. **Apply the tree.** Decide static, server island or client island for each component.
3. **Check common mistakes.** Flag client:visible on above-the-fold parts and hydrated navbars that need only a script.
4. **Check content.** Confirm glob or file loaders, Zod from astro/zod and schema validation.
5. **Check images and env.** Confirm Image or Picture with imports and astro:env for variables.
6. **Build.** Run the build and log findings.

Stop rule: Stops after one pull request per run.

## Permissions

- Writes: loops/astro-hydration-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/astro-hydration-review-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: Astro pull request. Verification: build and rules pass. Memory: loops/astro-hydration-review-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
