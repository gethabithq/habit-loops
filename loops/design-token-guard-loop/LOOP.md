---
name: design-system
title: Design System skill
repo: nextlevelbuilder/ui-ux-pro-max-skill
license: MIT
url: https://gethabit.dev/skills/nextlevelbuilder/design-system
---

# Design System skill

The design system skill builds three-layer design tokens (primitive, semantic, component), CSS variables, component state specs and token-based slide decks, with scripts to generate and validate tokens. For designers and frontend developers.

- Install the skill: `npx skills add nextlevelbuilder/ui-ux-pro-max-skill --skill design-system`
- Source: https://github.com/nextlevelbuilder/ui-ux-pro-max-skill/tree/HEAD/.claude/skills/design-system
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You set up design tokens and CSS variables; You want to catch hardcoded colors in code; You build brand-consistent slide decks.
Skip it when: You use a ready-made theme without tokens; You only need one quick mockup.

# Make it a habit: No hardcoded colors slip in.

When a pull request changes styles or slides, your agent runs the design-system checks: validate-tokens.cjs looks for hardcoded values in src/, and slide-token-validator.py checks slide HTML. It regenerates tokens.css when the token config changed and logs violations.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR changes styles (event; GitHub Actions or Claude Code routine; `pull_request paths: src/**, tokens.json, assets/design-tokens.json`)
- **Verification:** token validators pass. Hard checks: node scripts/validate-tokens.cjs --dir src/ finds no hardcoded values; slide-token-validator.py passes on changed slide HTML; generate-tokens.cjs builds tokens.css without error; every slide imports assets/design-tokens.css. On fail: retry, max 2 retries.
- **Memory:** token violation log at `loops/design-token-guard-loop/runs.md`. Read first: files with repeat token violations.

## Steps

1. **List changed files.** The agent lists changed style, component and slide files in the pull request.
2. **Regenerate tokens.** If the token config changed, it runs generate-tokens.cjs to rebuild tokens.css.
3. **Validate usage.** It runs validate-tokens.cjs --dir src/ to find raw hex and other hardcoded values.
4. **Validate slides.** For slide HTML it runs slide-token-validator.py and checks the design-tokens.css import.
5. **Fix with tokens.** It swaps hardcoded values for semantic or component tokens, using the brand and ui-styling skills where needed.
6. **Log violations.** It records each fixed file in the run log.

Stop rule: Stops after one pull request and at most 2 fix retries per run.

## Permissions

- Writes: src/**, tokens.css, loops/design-token-guard-loop/**
- Network: api.github.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/design-token-guard-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR changes styles. Verification: token validators pass. Memory: loops/design-token-guard-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
