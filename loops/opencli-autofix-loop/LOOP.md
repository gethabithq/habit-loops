---
name: opencli-autofix
title: OpenCLI AutoFix skill
repo: jackwener/OpenCLI
license: Apache-2.0
url: https://gethabit.dev/skills/jackwener/opencli-autofix
---

# OpenCLI AutoFix skill

The opencli autofix skill repairs broken OpenCLI adapters when a command fails: it collects a trace, patches the adapter, retries, and files an upstream issue after a verified fix. For agents and developers using opencli.

- Install the skill: `npx skills add jackwener/OpenCLI --skill opencli-autofix`
- Source: https://github.com/jackwener/OpenCLI/tree/HEAD/skills/opencli-autofix
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: An opencli command fails with a selector or API error; A site changed its DOM or response schema; You want the adapter fixed, not just the error reported.
Skip it when: The error is auth, browser connect or captcha; The feature was removed from the site.

# Make it a habit: Broken adapters fixed and retried.

When an opencli command fails, your agent collects a failure trace, rules out a soft block, patches only the adapter source, retries, and files an upstream issue after a verified fix. It stops on auth or captcha errors and after three repair rounds.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** opencli command fails (event; Claude Code; `opencli command exit non-zero`)
- **Verification:** retry passes. Hard checks: the same opencli command succeeds after the patch; verify/<cmd>.json fixtures are not loosened to pass; only the file at adapterSourcePath was changed. On fail: retry, max 2 retries.
- **Memory:** repair notes at `loops/opencli-autofix-loop/run-log.md`. Read first: adapters fixed before and the site notes in ~/.opencli/sites/<site>/notes.md.

## Steps

1. **Check hard stops.** The agent stops without touching code on AUTH_REQUIRED, BROWSER_CONNECT, captcha or rate limiting.
2. **Rule out a soft block.** It retries with another query and spot-checks in Chrome, since an empty result is often not an adapter bug.
3. **Collect the trace.** It reruns with --trace retain-on-failure and reads the summary.md front matter for adapterSourcePath.
4. **Explore the site.** It uses opencli browser, never the broken adapter, to find the new selector or API.
5. **Patch minimally.** It edits only the adapter source, keeps the output structure and prefers an API over DOM scraping.
6. **Verify and file.** It reruns the command, and after a passing retry asks you before filing an upstream GitHub issue.

Stop rule: Stops after a verified fix, or after 3 repair rounds, or at a hard-stop error.

## Permissions

- Writes: clis/**, loops/opencli-autofix-loop/**
- Network: github.com
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/opencli-autofix-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: opencli command fails. Verification: retry passes. Memory: loops/opencli-autofix-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
