---
name: design-guide
title: Paperclip Design Guide skill
repo: paperclipai/paperclip
license: MIT
url: https://gethabit.dev/skills/paperclipai/design-guide
---

# Paperclip Design Guide skill

The Paperclip Design Guide skill covers the Paperclip UI design system: tokens, typography scale, status and priority systems, component tiers, composition patterns, layout and the /design-guide showcase page. For contributors to the Paperclip frontend.

- Install the skill: `npx skills add paperclipai/paperclip --skill design-guide`
- Source: https://github.com/paperclipai/paperclip/tree/HEAD/.claude/skills/design-guide
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You add a Paperclip UI component; You style a new page; You update the design guide page.
Skip it when: You work outside the Paperclip UI; You change only backend code.

# Make it a habit: Keep components and design guide synced.

When UI components change, your agent checks the Paperclip rules: semantic tokens, the typography scale, StatusBadge and StatusIcon for status colors, minimal shadows and radii, and that every new or changed component appears on the /design-guide page and in the component index.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** UI components change (event; Claude Code routine; `pull request touches ui/src/components or ui/src/pages`)
- **Verification:** design rules and guide. Hard checks: every new reusable component appears in DesignGuide.tsx; every new component is listed in references/component-index.md; no shadow-md or heavier and no rounded-2xl or larger; build passes. On fail: retry, max 1 retries.
- **Memory:** design guide page at `ui/src/pages/DesignGuide.tsx`. Read first: sections already on the design guide page.

## Steps

1. **Load companion skills.** Your agent uses frontend-design and web-design-guidelines alongside this guide.
2. **Check tokens.** It checks colors use CSS variable tokens, not raw hex or rgb.
3. **Check typography.** It checks text uses the set scale, not ad hoc styles.
4. **Check status.** It checks status colors come from StatusBadge and StatusIcon.
5. **Update the guide.** It adds or updates sections on /design-guide with variants, sizes and states.
6. **Update the index.** It adds new components to references/component-index.md and builds.

Stop rule: Stops after 5 components or one retry per run.

## Permissions

- Writes: ui/src/**, references/component-index.md
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`ui/src/pages/DesignGuide.tsx`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: UI components change. Verification: design rules and guide. Memory: ui/src/pages/DesignGuide.tsx. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
