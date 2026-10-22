---
name: sanity-migration
title: Sanity Migration skill
repo: sanity-io/agent-toolkit
license: MIT
url: https://gethabit.dev/skills/sanity-io/sanity-migration
---

# Sanity Migration skill

The sanity migration skill plans, builds and reviews moves into Sanity from AEM, Contentful, Strapi, Webflow, WordPress, Payload, Drupal or Markdown, with Portable Text conversion, asset migration, redirects and validation.

- Install the skill: `npx skills add sanity-io/agent-toolkit --skill sanity-migration`
- Source: https://github.com/sanity-io/agent-toolkit/tree/HEAD/skills/sanity-migration
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You move a site from another CMS to Sanity; You convert HTML or Markdown to Portable Text; You plan redirects and cutover.
Skip it when: You already run on Sanity with no import; You only change one document.

# Make it a habit: Migration reruns converge, checks pass.

During a CMS move to Sanity, your agent reruns the deterministic migration scripts each night against a fresh source snapshot, then runs count, sample, reference and redirect checks. It stops to ask you when scope or access is unclear and keeps a validation summary.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** Nightly during migration (schedule; Claude Code routine or cron; `0 2 * * *`)
- **Verification:** migration checks, you confirm. Hard checks: document counts match the content inventory; sample checks pass on migrated documents; every reference resolves to an imported document; legacy routes have working redirects; no asset points at a legacy CDN URL. On fail: notify, max 1 retries.
- **Memory:** validation summary at `loops/sanity-migration-rerun-loop/validation.md`. Read first: last counts, per-document quality issues and open questions.

## Steps

1. **Read the guides.** The agent reads references/general.md and the guide for the source platform.
2. **Plan.** It keeps a short plan for access, scope, schema, extraction, transform, import, validation, redirects and cutover.
3. **Stop and ask.** It asks you before coding when access, target dataset, scope, media or schema is unclear.
4. **Snapshot.** It saves the extracted source data to disk before transforming it.
5. **Transform and import.** It converts rich text to Portable Text and imports with stable IDs via createOrReplace, createIfNotExists or sanity datasets import --replace.
6. **Validate.** It runs count, sample, reference and redirect checks and updates the validation summary.

Stop rule: Stops after one full rerun per night, with 1 retry on a failed import.

## Permissions

- Writes: migration scripts folder, source snapshot folder, loops/sanity-migration-rerun-loop/**
- Network: the source CMS API, the target Sanity project
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/sanity-migration-rerun-loop/validation.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: Nightly during migration. Verification: migration checks, you confirm. Memory: loops/sanity-migration-rerun-loop/validation.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
