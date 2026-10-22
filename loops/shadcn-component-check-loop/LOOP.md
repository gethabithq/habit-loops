---
name: shadcn-ui
title: shadcn/ui skill
repo: google-labs-code/stitch-skills
license: Apache-2.0
url: https://gethabit.dev/skills/google-labs-code/shadcn-ui
---

# shadcn/ui skill

The shadcn/ui skill helps frontend developers find, install and customize shadcn/ui components with Tailwind CSS and Radix UI or Base UI, including theming, variants, blocks and fixes for common setup errors.

- Install the skill: `npx skills add google-labs-code/stitch-skills --skill shadcn-ui`
- Source: https://github.com/google-labs-code/stitch-skills/tree/HEAD/plugins/stitch-build/skills/shadcn-ui
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You add shadcn/ui components to a React app; You set up components.json or theme variables; Imports or styles break after install.
Skip it when: Your project does not use Tailwind CSS; You want a packaged npm component library.

# Make it a habit: New UI components ship type-safe.

When a pull request adds or changes files in components/ui, your agent reviews them with the shadcn-ui skill: cn() for classes, wrappers outside components/ui, ARIA kept. Then tsc --noEmit and your linter must pass. A log keeps the components checked.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR changes components/ui (event; GitHub Actions or Claude Code routine; `pull_request paths: components/ui/**`)
- **Verification:** types and lint pass. Hard checks: tsc --noEmit passes; project linter passes; components.json exists and its aliases resolve; custom wrappers live in components/, not components/ui/. On fail: retry, max 2 retries.
- **Memory:** component check log at `loops/shadcn-component-check-loop/runs.md`. Read first: components already checked and open issues.

## Steps

1. **List changed components.** The agent reads the diff and lists new or changed files in components/ui.
2. **Check metadata.** It uses get_component_metadata to confirm each component's dependencies are in package.json.
3. **Review the code.** It checks cn() for class merging, cva for variants and ARIA attributes kept.
4. **Check wrappers.** It makes sure custom wrappers sit in components/ and not in components/ui/.
5. **Type check and lint.** It runs tsc --noEmit and the linter and fixes errors it caused.
6. **Log results.** It writes the checked components and any open accessibility notes to the run log.

Stop rule: Stops after one pull request and at most 2 fix retries per run.

## Permissions

- Writes: components/**, loops/shadcn-component-check-loop/**
- Network: api.github.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/shadcn-component-check-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR changes components/ui. Verification: types and lint pass. Memory: loops/shadcn-component-check-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
