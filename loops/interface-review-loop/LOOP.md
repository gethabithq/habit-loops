---
name: better-interface
title: Better Interface skill
repo: jakubkrehel/skills
license: MIT
url: https://gethabit.dev/skills/jakubkrehel/better-interface
---

# Better Interface skill

The better interface skill runs one review across accessibility, layout, writing, typography, color and UI polish by routing to the better-* skills and merging one ranked verdict.

- Install the skill: `npx skills add jakubkrehel/skills --skill better-interface`
- Source: https://github.com/jakubkrehel/skills/tree/HEAD/skills/better-interface
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You want one review across all UI disciplines; You audit a full user flow; You need findings ranked by user impact.
Skip it when: You want a review of a branch or pull request; The other better-* skills are not installed.

# Make it a habit: One ranked verdict across six domains.

On a schedule, your agent reviews one complete flow by running six better-* skills in order and merging their evidence into one ranked table of at most 15 findings. Escalation triggers are always HIGH. Open findings are logged for the next run.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly flow review (schedule; Claude Code routine; `0 9 * * 1`)
- **Verification:** evidence + coverage check. Hard checks: every finding cites path/to/file:line; no more than 15 findings; each domain is reviewed or marked Not reviewed; escalation triggers are rated HIGH. On fail: notify, max 0 retries.
- **Memory:** findings by root cause at `loops/interface-review-loop/run-log.md`. Read first: open findings, flows already covered and domains marked Not reviewed.

## Steps

1. **Resolve scope.** The agent picks one complete flow and states what it left out.
2. **Recon.** It finds the framework, tokens and viewports, and reads CONTRIBUTING.md, AGENTS.md or CLAUDE.md if present.
3. **Run domain skills.** It loads better-accessibility, better-layout, better-writing, better-typography, better-colors and better-ui in that order.
4. **Rank.** Findings get one shared HIGH, MEDIUM or LOW scale, with triggers first.
5. **Pick cheap fixes.** Each fix starts from delete, then the platform, then project tokens, before adding anything.
6. **Verify and report.** It runs safe project checks and writes one table in the review-format.md format.

Stop rule: One flow per run, at most 15 findings.

## Permissions

- Writes: loops/interface-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/interface-review-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly flow review. Verification: evidence + coverage check. Memory: loops/interface-review-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
