---
name: chakra-ui-refactor
title: Chakra UI Refactor skill
repo: chakra-ui/chakra-ui
license: MIT
url: https://gethabit.dev/skills/chakra-ui/chakra-ui-refactor
---

# Chakra UI Refactor skill

Chakra ui refactor reviews, converts and improves UI code with Chakra UI v3, from plain HTML, Tailwind, CSS Modules or styled-components, checking accessibility, responsiveness, tokens and v3 API use. For React developers using Chakra UI.

- Install the skill: `npx skills add chakra-ui/chakra-ui --skill chakra-ui-refactor`
- Source: https://github.com/chakra-ui/chakra-ui/tree/HEAD/skills/chakra-ui-refactor
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You review a Chakra component; You convert Tailwind to Chakra; You migrate Chakra v2 code to v3.
Skip it when: You do not use Chakra UI; You need a new design system.

# Make it a habit: Components stay accessible and v3-correct.

On every pull request that touches UI components, your agent reviews them with the Chakra UI v3 checklist: accessibility, responsiveness, v3 API names, semantic tokens, structure and maintainability. It reports critical issues with minimal fixes and logs v2 leftovers.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** component files change (event; GitHub Actions or Claude Code routine; `pull_request paths: src/components/**`)
- **Verification:** critical issue count. Hard checks: no v2 props like isDisabled or colorScheme remain in changed files; every icon-only button has an aria-label; the count of critical findings is zero. On fail: notify, max 0 retries.
- **Memory:** UI review log at `loops/chakra-ui-review-loop/log.md`. Read first: v2 patterns still left and repeated patterns to extract.

## Steps

1. **Orient.** Check package.json for the Chakra version and note the framework and source type.
2. **Check accessibility.** Look for missing labels, keyboard access, heading order and Field.Root usage.
3. **Check API and tokens.** Flag v2 props and patterns, hardcoded colors and inline style props.
4. **Check structure.** Flag deep nesting, manual spacing and the wrong layout primitive.
5. **Report.** Group findings as critical, improvements and optional, with a minimal fix for each critical one.

Stop rule: Stops after the changed components of one pull request, at most 20 files.

## Permissions

- Writes: loops/chakra-ui-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/chakra-ui-review-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: component files change. Verification: critical issue count. Memory: loops/chakra-ui-review-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
