---
name: generate-translations
title: Generate Translations skill
repo: payloadcms/payload
license: MIT
url: https://gethabit.dev/skills/payloadcms/generate-translations
---

# Generate Translations skill

The generate translations skill helps Payload contributors add English keys to core or plugin packages and run the pnpm scripts that translate them into every supported language.

- Install the skill: `npx skills add payloadcms/payload --skill generate-translations`
- Source: https://github.com/payloadcms/payload/tree/HEAD/.agents/skills/generate-translations
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You add new UI text to Payload; A plugin needs translated labels; A plugin lacks a translations folder.
Skip it when: You do not work on Payload; No OPENAI_KEY is available.

# Make it a habit: Every new key gets translated.

When an English en.ts file in Payload core or a plugin changes, your agent adds needed client keys and runs the matching generateTranslations script from tools/scripts. A check confirms every new key now exists in all languages.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** English keys change (event; GitHub Actions or Claude Code routine; `push touching packages/translations/src/languages/en.ts or a plugin's src/translations/languages/en.ts`)
- **Verification:** all languages have keys. Hard checks: the generateTranslations script exits without error; every new English key appears in all language files; browser-side keys are listed in clientKeys.ts. On fail: notify, max 1 retries.
- **Memory:** translation run log at `loops/payload-translations-loop/runs.md`. Read first: keys already translated in earlier runs.

## Steps

1. **Detect new keys.** A change to an English en.ts file in core or a plugin starts the run.
2. **Add client keys.** Keys used in the browser get a colon-notation entry in packages/translations/src/clientKeys.ts.
3. **Check plugin folder.** For a plugin, confirm packages/plugin-{name}/src/translations exists, or ask you whether to scaffold it.
4. **Generate core.** From tools/scripts, pnpm generateTranslations:core fills every other language.
5. **Generate plugins.** Each touched plugin runs its own pnpm generateTranslations:plugin-{name} script.
6. **Check coverage.** Every new English key must now show up in all language files.

Stop rule: Stops after core plus three plugins per run.

## Permissions

- Writes: packages/translations/src/**, packages/plugin-*/src/translations/**, tools/scripts/**, loops/payload-translations-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/payload-translations-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: English keys change. Verification: all languages have keys. Memory: loops/payload-translations-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
