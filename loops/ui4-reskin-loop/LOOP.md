---
name: ui4
title: UI4 skill
repo: payloadcms/payload
license: MIT
url: https://gethabit.dev/skills/payloadcms/ui4
---

# UI4 skill

The ui4 skill helps Payload UI developers reskin components to match a Figma design: icon scan, SCSS to CSS migration, variant matrix, token-based restyle, Playwright checks and variant e2e tests.

- Install the skill: `npx skills add payloadcms/payload --skill ui4`
- Source: https://github.com/payloadcms/payload/tree/HEAD/.agents/skills/ui4
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You reskin a Payload UI component; You migrate SCSS to CSS tokens; You match a component to Figma.
Skip it when: You have no Figma URL; You do not work in the Payload repo.

# Make it a habit: One component reskinned to match Figma.

For each Payload UI component on the board, your agent scans icons, migrates SCSS to CSS, maps every Figma variant, restyles with tokens, verifies each state with Playwright screenshots, gets your confirmation, writes variant e2e tests and runs ui4-review.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** next component on board (manual; Claude Code routine; `run with /ui4 and a Figma URL for the next component`)
- **Verification:** you confirm, tests pass. Hard checks: index.scss is deleted and index.css is wrapped in @layer payload-default; every Figma variant state was screenshotted and compared; pnpm run test:e2e --grep for the component's variants passes; ui4-review reports no unfixed violations. On fail: retry, max 2 retries.
- **Memory:** components to reskin at `loops/ui4-reskin-loop/board.md`. Read first: components done, in progress and their Figma URLs.

## Steps

1. **Get the Figma URL.** Ask for the Figma URL if it is missing.
2. **Scan icons.** Compare icon imports with packages/ui/src/icons/ and flag missing icons for you.
3. **Migrate SCSS.** Convert to index.css with tokens, flat BEM selectors and @layer payload-default.
4. **Map variants.** Build a variant matrix from mcp_figma2_get_metadata and get_design_context.
5. **Restyle.** Apply tokens from packages/ui/src/css/ and add test collection variants.
6. **Verify states.** Screenshot every state with Playwright and fix until each matches Figma.
7. **You confirm.** Share the screenshot and dev server URL and wait for your approval.
8. **Test and review.** Write variant e2e tests, run them, then run the ui4-review skill.

Stop rule: Stops after one component per run, with at most 2 restyle rounds before asking you.

## Permissions

- Writes: packages/ui/src/**, test/v4/**, loops/ui4-reskin-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/ui4-reskin-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: next component on board. Verification: you confirm, tests pass. Memory: loops/ui4-reskin-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
