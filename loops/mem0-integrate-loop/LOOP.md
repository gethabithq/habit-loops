---
name: mem0-integrate
title: Mem0 Integrate skill
repo: mem0ai/mem0
license: Apache-2.0
url: https://gethabit.dev/skills/mem0ai/mem0-integrate
---

# Mem0 Integrate skill

The mem0 integrate skill adds Mem0 memory to an existing Python or TypeScript backend with a test-first pipeline, approval gates and a feature flag. For developers who want a clean, reviewable integration branch.

- Install the skill: `npx skills add mem0ai/mem0 --skill mem0-integrate`
- Source: https://github.com/mem0ai/mem0/tree/HEAD/skills/mem0-integrate
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: adding Mem0 memory to an existing repo; you want an opt-in, flagged integration; you need reviewable separate commits.
Skip it when: the repo is frontend only; you only want general Mem0 SDK usage.

# Make it a habit: Mem0 added behind a feature flag.

On demand, your agent wires Mem0 into a repo test-first: goal doc and plan you approve, failing tests, a reviewed diff, four local commits, then a heal loop with mem0-test-integration. Goal, plan and summary stay in .mem0-integration/.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** you ask to integrate (manual; Claude Code routine; `/mem0-integrate`)
- **Verification:** approvals, tests, heal loop. Hard checks: git index is clean before start; new write and read tests fail before implementation; all pre-existing tests pass with MEM0_ENABLED set and unset; /mem0-test-integration --ci passes; exit code is 0. On fail: stop, max 2 retries.
- **Memory:** integration artifacts folder at `.mem0-integration/`. Read first: repo-summary.md, goal.md and plan.md from earlier runs.

## Steps

1. **Check preconditions.** Your agent refuses to start on a dirty repo, an unknown language or a frontend-only repo.
2. **Read the repo.** It detects the language, writes repo-summary.md and you pick a backend surface.
3. **Pick product.** It recommends Platform or OSS, checks MEM0_API_KEY or OPENAI_API_KEY, and fetches the canonical docs.
4. **Goal and plan.** It writes goal.md and plan.md with the delegated skill, and you approve each one.
5. **Tests first.** It writes failing write and read tests in the repo's own framework.
6. **Implement.** A fresh subagent builds the change and the diff is reviewed against plan.md and goal.md.
7. **Commit.** It commits on a mem0-integrate branch in four separate commits and never pushes.
8. **Heal.** It runs /mem0-test-integration --ci and fixes failures with a bounded subagent, or stops on a pre-existing failure.

Stop rule: Stops after one repo per run: 3 rejections per gate, 3 review loops, 3 heal attempts per category unless --heal-max says otherwise.

## Permissions

- Writes: .mem0-integration/**, .gitignore, repo source tree on a local feature branch
- Network: docs.mem0.ai, mcp.mem0.ai, raw.githubusercontent.com, github.com
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`.mem0-integration/`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: you ask to integrate. Verification: approvals, tests, heal loop. Memory: .mem0-integration/. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
