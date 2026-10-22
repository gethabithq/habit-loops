---
name: write-product-spec
title: Write Product Spec skill
repo: warpdotdev/common-skills
license: MIT
url: https://gethabit.dev/skills/warpdotdev/write-product-spec
---

# Write Product Spec skill

The write product spec skill writes PRODUCT.md for a significant feature: a short summary and an exhaustive Behavior section of numbered, testable invariants from the user's view.

- Install the skill: `npx skills add warpdotdev/common-skills --skill write-product-spec`
- Source: https://github.com/warpdotdev/common-skills/tree/HEAD/.agents/skills/write-product-spec
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You need a PRD before building; Feature behavior is ambiguous; Agents will implement from the spec.
Skip it when: The change is a trivial fix; You need an implementation plan, not behavior.

# Make it a habit: Behavior written as testable invariants.

When a feature needs a spec, your agent gathers the missing context with you, asks about a Figma mock and writes specs/<id>/PRODUCT.md with a numbered Behavior section. It checks the required sections and hands off to write-tech-spec next.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** feature needs a spec (event; Claude Code routine or GitHub Actions; `issues.labeled == spec, or a Linear ticket for a significant feature`)
- **Verification:** your answers + section check. Hard checks: specs/<id>/PRODUCT.md exists; Summary and Behavior sections are present; Behavior is a numbered list; no Validation, Success criteria or Testing section. On fail: notify, max 0 retries.
- **Memory:** product spec at `specs/<id>/PRODUCT.md`. Read first: the existing PRODUCT.md and DECISIONS.md if present.

## Steps

1. **Pick the id.** Use a Linear ticket, a gh- issue id or a kebab-case feature name you give.
2. **Gather context.** Ask with ask_user_question for users, key behaviors and edge cases that are missing.
3. **Ask for Figma.** For UI features, ask if a mock exists and record the link or Figma: none provided.
4. **Write Behavior.** Write numbered invariants for states, inputs, errors, edge cases and focus.
5. **Keep framing thin.** Add Problem, Goals or Open questions only when they add something.
6. **Hand off.** Once PRODUCT.md is agreed, invoke write-tech-spec for TECH.md.

Stop rule: One feature spec per run.

## Permissions

- Writes: specs/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`specs/<id>/PRODUCT.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: feature needs a spec. Verification: your answers + section check. Memory: specs/<id>/PRODUCT.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
