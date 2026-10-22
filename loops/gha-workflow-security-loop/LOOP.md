---
name: gha-security-review
title: GHA Security Review skill
repo: getsentry/skills
license: Apache-2.0
url: https://gethabit.dev/skills/getsentry/gha-security-review
---

# GHA Security Review skill

Gha security review audits GitHub Actions workflows for exploitable bugs like pwn requests, expression injection, credential theft and supply chain attacks, reporting only traced findings with concrete exploit scenarios. For teams securing CI.

- Install the skill: `npx skills add getsentry/skills --skill gha-security-review`
- Source: https://github.com/getsentry/skills/tree/HEAD/skills/gha-security-review
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You review GitHub Actions workflows; You add a pull_request_target job; You audit CI before release.
Skip it when: You need a general code review; Your CI is not GitHub Actions.

# Make it a habit: Exploitable workflow bugs caught before merge.

When a pull request touches GitHub Actions workflows or actions, your agent classifies triggers, runs the eight vulnerability checks, traces every attack path and reports only high and medium findings an external attacker could exploit. A log keeps findings and cleared workflows.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** workflow file changes (event; GitHub Actions or Claude Code routine; `pull_request paths: .github/workflows/**, action.yml`)
- **Verification:** traced findings only. Hard checks: every HIGH finding has entry point, payload, execution, impact and PoC sketch; every reviewed workflow appears under findings or reviewed and cleared; the count of HIGH findings is zero. On fail: notify, max 0 retries.
- **Memory:** workflow review log at `loops/gha-workflow-security-loop/log.md`. Read first: open findings and workflows already cleared.

## Steps

1. **Classify triggers.** List each workflow's triggers and load only the matching references.
2. **Run the checks.** Check pwn requests, expression injection, comment commands, credentials, config poisoning, supply chain, permissions and runners.
3. **Skip safe patterns.** Drop patterns the skill lists as safe, like expressions in if: or with: inputs.
4. **Trace attack paths.** Read the full YAML and confirm trigger, attacker control and missing mitigations.
5. **Report.** Write findings, needs-verification items and cleared workflows, or report zero findings.

Stop rule: Stops after the changed workflows of one pull request.

## Permissions

- Writes: loops/gha-workflow-security-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/gha-workflow-security-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: workflow file changes. Verification: traced findings only. Memory: loops/gha-workflow-security-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
