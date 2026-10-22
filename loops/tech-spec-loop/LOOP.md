---
name: write-tech-spec
title: Write Tech Spec skill
repo: warpdotdev/common-skills
license: MIT
url: https://gethabit.dev/skills/warpdotdev/write-tech-spec
---

# Write Tech Spec skill

The write tech spec skill writes TECH.md for a significant feature after researching the codebase: context with commit-pinned references, proposed changes, testing mapped to product behavior and a parallel plan.

- Install the skill: `npx skills add warpdotdev/common-skills --skill write-tech-spec`
- Source: https://github.com/warpdotdev/common-skills/tree/HEAD/.agents/skills/write-tech-spec
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: A feature spans several modules; Reviewers need the plan before the code; A PRODUCT.md is already agreed.
Skip it when: The change is a single obvious fix; The approach is too uncertain to plan yet.

# Make it a habit: Plans grounded in the real code.

When a PRODUCT.md is agreed, your agent reads it, inspects the code, pins references to a commit SHA and writes specs/<id>/TECH.md with context, changes, testing and parallelization. A check confirms the required sections and that tests map to Behavior items.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** product spec approved (event; Claude Code routine or GitHub Actions; `specs/<id>/PRODUCT.md merged or approved`)
- **Verification:** required sections present. Hard checks: specs/<id>/TECH.md exists next to PRODUCT.md; Context, Proposed changes and Testing and validation sections are present; code references carry a commit SHA; each key Behavior invariant maps to a test or check. On fail: notify, max 1 retries.
- **Memory:** tech spec at `specs/<id>/TECH.md`. Read first: PRODUCT.md, the current TECH.md and DECISIONS.md if present.

## Steps

1. **Read the product spec.** The agent reads PRODUCT.md and uses the same id for the directory.
2. **Research the code.** It inspects the relevant files, types and data flow, and captures the commit with git rev-parse HEAD.
3. **Write context.** It describes the current system with commit-pinned file links.
4. **Propose changes.** It lists module changes, new types and tradeoffs that fit existing patterns.
5. **Plan testing.** It maps numbered Behavior items from PRODUCT.md to concrete tests and checks.
6. **Parallelization.** If run_agents exists, it proposes sub-agents with worktrees and branches, or says why not.

Stop rule: One TECH.md per run, one fix retry on missing sections.

## Permissions

- Writes: specs/**
- Network: github.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`specs/<id>/TECH.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: product spec approved. Verification: required sections present. Memory: specs/<id>/TECH.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
