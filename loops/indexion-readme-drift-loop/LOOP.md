---
name: indexion-readme
title: Indexion README skill
repo: trkbt10/indexion-skills
license: Apache-2.0
url: https://gethabit.dev/skills/trkbt10/indexion-readme
---

# Indexion README skill

Indexion readme builds project READMEs from templates, doc comments, static prose and per-package READMEs, then verifies edits with plan drift. For maintainers of projects that use the indexion CLI to assemble documentation.

- Install the skill: `npx skills add trkbt10/indexion-skills --skill indexion-readme`
- Source: https://github.com/trkbt10/indexion-skills/tree/HEAD/skills/indexion-readme
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You assemble a root README from parts; You add a new command package; You want to prove a README edit is additive.
Skip it when: Your project does not use indexion; You only review existing docs quality.

# Make it a habit: README changes stay purely additive.

When a pull request touches docs or packages, your agent regenerates per-package READMEs, assembles the root README with indexion doc readme and runs indexion plan drift against the previous version. A run log keeps the drift result of each run.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** docs or package change (event; GitHub Actions; `pull_request paths: docs/**, cmd/**, src/**`)
- **Verification:** plan drift guard. Hard checks: indexion plan drift --vocab-threshold=0.05 exits 0; drift terms missing from the previous README are (none); git status shows no unintended per-package READMEs. On fail: notify, max 0 retries.
- **Memory:** drift run log at `loops/indexion-readme-drift-loop/log.md`. Read first: last drift result and packages that are hand-maintained.

## Steps

1. **Inspect the setup.** Check for a README.md symlink, a doc.json and an .indexion.toml to see how the README is built.
2. **Generate package READMEs.** Run indexion doc readme --per-package on the package folders to create missing skeletons without overwriting.
3. **Write the prose.** Fill the Overview, Usage, Options and Examples sections of new package READMEs by hand.
4. **Assemble the root.** Run indexion doc readme --config=doc.json to build the root README.
5. **Check drift.** Snapshot the previous README with git show and compare it with indexion plan drift.
6. **Clean up.** Revert per-package READMEs that template mode created in packages you did not touch.

Stop rule: Stops after one assembly and one drift check per run.

## Permissions

- Writes: README.md, cmd/**/README.md, src/**/README.md, docs/**, loops/indexion-readme-drift-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/indexion-readme-drift-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: docs or package change. Verification: plan drift guard. Memory: loops/indexion-readme-drift-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
