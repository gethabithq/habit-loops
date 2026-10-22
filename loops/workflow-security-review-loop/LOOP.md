---
name: ci-cd-security
title: CI/CD security skill
repo: superagent-ai/skills
license: MIT
url: https://gethabit.dev/skills/superagent-ai/ci-cd-security
---

# CI/CD security skill

The ci/cd security skill reviews GitHub Actions workflow YAML for risky triggers, permissions, action pinning and injection patterns, with no tools to install, for maintainers hardening their pipelines.

- Install the skill: `npx skills add superagent-ai/skills --skill ci-cd-security`
- Source: https://github.com/superagent-ai/skills/tree/HEAD/skills/ci-cd-security
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: A pull request changes a workflow; You harden an open source repo; You ask about pull_request_target.
Skip it when: Your CI is not GitHub Actions; You need org settings audited.

# Make it a habit: Catch risky CI workflow changes.

When a pull request touches .github/workflows/, your agent reads each changed YAML file, walks the nine rule passes and reports findings by severity with a fix. A log keeps open findings for the next review.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** workflow file changed (event; GitHub Actions or Claude Code routine; `pull_request paths .github/workflows/**`)
- **Verification:** all passes walked. Hard checks: all nine passes reported per file; every finding has severity and file line; no open P0 findings. On fail: notify, max 0 retries.
- **Memory:** open findings list at `loops/workflow-security-review-loop/findings.md`. Read first: open findings from earlier reviews.

## Steps

1. **Collect files.** Gather the changed files under .github/workflows/ from the pull request.
2. **Check triggers.** Review the on: block for risky triggers like pull_request_target and workflow_run.
3. **Check permissions.** Look for missing or broad permissions: blocks.
4. **Check pinning.** Review every uses: line for tag or branch pins.
5. **Check run blocks.** Look for untrusted values placed straight into run: scripts and fix them with env.
6. **Remaining passes.** Walk checkout, caching, artifacts, release and runner passes.
7. **Report.** List findings by severity, P0 first, with a rewrite, or say nothing fired and what was not checked.

Stop rule: Stops after ten workflow files per run.

## Permissions

- Writes: loops/workflow-security-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/workflow-security-review-loop/findings.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: workflow file changed. Verification: all passes walked. Memory: loops/workflow-security-review-loop/findings.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
