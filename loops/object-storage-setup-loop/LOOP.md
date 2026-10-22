---
name: extension-object-storage
title: Extension Object Storage skill
repo: caffeinelabs/skills
license: Apache-2.0
url: https://gethabit.dev/skills/caffeinelabs/extension-object-storage
---

# Extension Object Storage skill

The extension object storage skill helps Caffeine AI app builders store images, videos and files off-chain with on-chain references, using ExternalBlob on backend and frontend.

- Install the skill: `npx skills add caffeinelabs/skills --skill extension-object-storage`
- Source: https://github.com/caffeinelabs/skills/tree/HEAD/skills/extension-object-storage
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You build an image or video gallery on Caffeine; Your app stores large files; Uploads fail with 403 Invalid payload.
Skip it when: Your app is not built on Caffeine AI; You store only small text records.

# Make it a habit: File uploads keep working.

When the backend or frontend of a Caffeine app changes, your agent checks the four required object storage setup steps, looks for hand-written storage methods and Text file fields, and keeps a log of past findings.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** backend or frontend changed (event; GitHub Actions or Claude Code routine; `push touching src/backend/** or package.json`)
- **Verification:** four setup steps present. Hard checks: caffeineai-object-storage is listed under [dependencies] in src/backend/mops.toml; main.mo contains include MixinObjectStorage() imported from mo:caffeineai-object-storage/Mixin; no file field or upload parameter is typed Text instead of Storage.ExternalBlob; no hand-written _immutableObjectStorage* method exists; @caffeineai/object-storage is installed and uses ExternalBlob.fromBytes(bytes, file.type, file.name); build passes. On fail: notify, max 1 retries.
- **Memory:** storage check log at `loops/object-storage-setup-loop/run-log.md`. Read first: checks that failed in the last run.

## Steps

1. **Read the log.** The agent reads which checks failed last time.
2. **Check mops package.** It confirms caffeineai-object-storage sits in src/backend/mops.toml.
3. **Check the mixin.** It confirms main.mo includes MixinObjectStorage() from the mops package, not a relative path.
4. **Check field types.** It flags any file field typed Text and any custom _immutableObjectStorage method.
5. **Check frontend.** It confirms the npm package is installed and file type comes from filename or mimeType, never the URL.
6. **Log and report.** It writes each result to the run log and notifies you on a fail.

Stop rule: Stops after one pass over the four setup steps per run, with at most one retry.

## Permissions

- Writes: loops/object-storage-setup-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/object-storage-setup-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: backend or frontend changed. Verification: four setup steps present. Memory: loops/object-storage-setup-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
