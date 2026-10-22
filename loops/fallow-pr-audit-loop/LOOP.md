---
name: fallow
title: Fallow skill
repo: fallow-rs/fallow-skills
license: MIT
url: https://gethabit.dev/skills/fallow-rs/fallow
---

# Fallow skill

The fallow skill gives an agent codebase intelligence for TypeScript and JavaScript: changed-code risk, dead code, duplication, circular dependencies, complexity hotspots and architecture boundaries, all as machine-readable JSON. For developers guarding code quality.

- Install the skill: `npx skills add fallow-rs/fallow-skills --skill fallow`
- Source: https://github.com/fallow-rs/fallow-skills/tree/HEAD/fallow/skills/fallow
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You audit PR risk before merge; You hunt unused code or dependencies; You set up a CI quality gate.
Skip it when: You debug a runtime error; The project is not JavaScript or TypeScript.

# Make it a habit: Every PR gets a risk verdict.

When a pull request opens, the agent runs fallow audit against the base branch for a pass, warn or fail verdict on introduced risk, reads the walkthrough guide and writes a judgment that fallow checks. Findings go into a log and the audit exit code gates the PR.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** pull request opened (event; GitHub Actions or Claude Code routine; `pull_request opened or synchronize`)
- **Verification:** audit verdict and judgment. Hard checks: fallow audit --base <ref> exits with a pass, warn or fail per its exit ladder; the judgment file only cites ids fallow emitted; fallow does not mark the judgment stale. On fail: notify, max 1 retries.
- **Memory:** audit findings log at `loops/fallow-pr-audit-loop/log.md`. Read first: verdicts and findings from earlier pull requests.

## Steps

1. **Run the audit.** Run fallow audit --base against the target branch with --format json --quiet.
2. **Read the guide.** Run fallow audit --walkthrough-guide and read its decisions and change anchors.
3. **Write a judgment.** Write a judgment file citing only ids the guide emitted, keeping it outside the project tree.
4. **Let fallow check it.** Run fallow audit --walkthrough-file so fallow validates the judgment against the live graph.
5. **Report accepted.** Report only the accepted judgments and add the verdict to the log.

Stop rule: Stops after one pull request per run and at most 1 retry.

## Permissions

- Writes: loops/fallow-pr-audit-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/fallow-pr-audit-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: pull request opened. Verification: audit verdict and judgment. Memory: loops/fallow-pr-audit-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
