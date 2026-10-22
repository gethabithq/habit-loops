---
name: sanity-best-practices
title: Sanity Best Practices skill
repo: sanity-io/agent-toolkit
license: MIT
url: https://gethabit.dev/skills/sanity-io/sanity-best-practices
---

# Sanity Best Practices skill

The sanity best practices skill gives Sanity developers topic guides for schemas, GROQ, TypeGen, Visual Editing, Portable Text, localization, migrations, Functions and framework integrations.

- Install the skill: `npx skills add sanity-io/agent-toolkit --skill sanity-best-practices`
- Source: https://github.com/sanity-io/agent-toolkit/tree/HEAD/skills/sanity-best-practices
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You design or change Sanity schemas; You write or tune GROQ queries; You wire Sanity into a frontend framework.
Skip it when: Your CMS is not Sanity; You only edit content in the Studio.

# Make it a habit: Sanity changes follow house rules.

When a pull request touches Sanity schemas, GROQ queries or Studio code, your agent loads the one or two matching topic guides and reviews the diff against them. It checks the global ID and video rules and that the build passes, and logs findings per guide.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR touches Sanity code (event; GitHub Actions or Claude Code routine; `pull_request paths: schema, GROQ queries, Studio structure, sanity.blueprint.ts`)
- **Verification:** rules + build check. Hard checks: no new ordinary document gets a hand-made or slug-derived _id; relations use reference fields; no user-facing video served from a file asset; build passes. On fail: notify, max 0 retries.
- **Memory:** findings per guide at `loops/sanity-review-loop/run-log.md`. Read first: past findings and which topic guides they came from.

## Steps

1. **Read the diff.** The run starts from the changed files in the pull request.
2. **Pick the guide.** The agent picks the single framework or topic guide that fits, like groq, schema or nextjs.
3. **Add only if needed.** It opens a second reference file only when the change crosses concerns.
4. **Check global rules.** It checks IDs, reference fields and video handling against the skill's global rules.
5. **Run the build.** The project build must pass before the review is posted.
6. **Log findings.** Findings go to the run log with the guide that backs each one.

Stop rule: One pull request per run, at most two topic guides loaded.

## Permissions

- Writes: loops/sanity-review-loop/**
- Network: api.github.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/sanity-review-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR touches Sanity code. Verification: rules + build check. Memory: loops/sanity-review-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
