---
name: heroui-native
title: HeroUI Native skill
repo: heroui-inc/heroui
license: Apache-2.0
url: https://gethabit.dev/skills/heroui-inc/heroui-native
---

# HeroUI Native skill

The heroui native skill helps React Native developers build mobile UIs with HeroUI Native components, Uniwind styling and HSL themes, and fetches current component docs before any code is written.

- Install the skill: `npx skills add heroui-inc/heroui --skill heroui-native`
- Source: https://github.com/heroui-inc/heroui/tree/HEAD/skills/heroui-native
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You build a React Native app with HeroUI; You set up Uniwind and themes; You need current component props.
Skip it when: You build for the web with HeroUI React; Your app uses another UI library.

# Make it a habit: HeroUI Native code stays native.

When a pull request changes mobile UI, your agent fetches the HeroUI Native docs for each touched component and checks the code for web patterns, flat props, onClick and raw colors. A notes file keeps which components were checked.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR changes mobile UI (event; GitHub Actions or Claude Code routine; `pull_request.opened or synchronize, paths: *.tsx, global.css`)
- **Verification:** native pattern checks. Hard checks: no import from @heroui/react; no onClick on heroui-native components; Card uses Card.Body, never Card.Content; theme colors in global.css use HSL, not oklch; app is wrapped in GestureHandlerRootView and HeroUINativeProvider; build passes. On fail: notify, max 0 retries.
- **Memory:** component usage notes at `loops/heroui-native-check-loop/notes.md`. Read first: components already checked and the slugs of their docs.

## Steps

1. **Pick up change.** A pull request that touches .tsx files or global.css starts the run.
2. **List components.** The agent runs node scripts/list_components.mjs to get the exact slugs of the touched components.
3. **Fetch the docs.** It runs node scripts/get_component_docs.mjs for each touched component and node scripts/get_theme.mjs for the theme.
4. **Check patterns.** It looks for web patterns, flattened compound components, onClick and raw colors instead of semantic variants.
5. **Check setup.** It confirms Uniwind, the two providers and HSL theme variables are in place.
6. **Report and note.** Findings and checked components go into the notes file, and a failed check notifies you.

Stop rule: Stops after one pull request per run, with at most 15 components checked.

## Permissions

- Writes: loops/heroui-native-check-loop/**
- Network: heroui.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/heroui-native-check-loop/notes.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR changes mobile UI. Verification: native pattern checks. Memory: loops/heroui-native-check-loop/notes.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
