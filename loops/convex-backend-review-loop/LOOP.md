---
name: convex
title: Convex skill
repo: convex/agent-skills
license: Apache-2.0
url: https://gethabit.dev/skills/convex/convex
---

# Convex skill

The convex skill is the entry point for building on Convex: it routes agents to the right convex-* skill for new apps, code under convex/, added capabilities, reviews and live operations. For full-stack TypeScript developers.

- Install the skill: `npx skills add convex/agent-skills --skill convex`
- Source: https://github.com/convex/agent-skills/tree/HEAD/skills/convex
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: Your project uses Convex; You need a backend fast; You want authz and correctness reviews.
Skip it when: Your backend stack is already fixed elsewhere; You need no persistence.

# Make it a habit: Every Convex change reviewed and verified.

When a pull request changes files under convex/, your agent routes it through convex-expert, convex-reviewer, convex-authz and convex-verify, and needs tsc --noEmit to pass. A board keeps open findings so the next run starts from them.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR changes convex/ (event; GitHub Actions or Claude Code routine; `pull_request paths: convex/**`)
- **Verification:** typecheck and verify pass. Hard checks: tsc --noEmit passes; convex-verify tests pass, including wrong-user refusals; no open high findings from convex-authz. On fail: notify, max 1 retries.
- **Memory:** open Convex findings at `loops/convex-backend-review-loop/board.md`. Read first: open review and authz findings from earlier runs.

## Steps

1. **Check AI guidance.** If the project lacks current Convex AI guidance, recommend npx convex ai-files install first.
2. **Load the expert.** Consult convex-expert before reading or editing code under convex/.
3. **Review correctness.** Run convex-reviewer for security, validators, performance and pattern checks.
4. **Audit access.** Run convex-authz to find impersonation, missing ownership checks and leaking public queries.
5. **Verify behaviour.** Run convex-verify and tsc --noEmit to prove the change works for several mocked users.
6. **Update the board.** Add new findings to the board and close the ones the change fixed.

Stop rule: One pull request per run, at most one retry after a failed typecheck.

## Permissions

- Writes: loops/convex-backend-review-loop/**
- Network: docs.convex.dev, api.github.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/convex-backend-review-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR changes convex/. Verification: typecheck and verify pass. Memory: loops/convex-backend-review-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
