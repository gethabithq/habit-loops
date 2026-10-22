---
name: okf-knowledge-base
title: OKF Knowledge Base skill
repo: inkeep/open-knowledge-skills
license: MIT
url: https://gethabit.dev/skills/inkeep/okf-knowledge-base
---

# OKF Knowledge Base skill

The okf knowledge base skill guides an agent through the Open Knowledge Format v0.2: concept files, types, provenance, links, indexes and logs. For teams who keep agent-readable knowledge in Markdown bundles.

- Install the skill: `npx skills add inkeep/open-knowledge-skills --skill okf-knowledge-base`
- Source: https://github.com/inkeep/open-knowledge-skills/tree/HEAD/skills/starter-packs/okf-knowledge-base/okf-knowledge-base
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You create an OKF bundle; The okf plugin shows warnings; You add provenance to concepts.
Skip it when: Your docs are not in OKF; You only need a plain README.

# Make it a habit: Knowledge bundle stays conformant.

Every week your agent reads your Open Knowledge Format bundle from the root index.md, fixes frontmatter and provenance against the OKF v0.2 rules, clears okf plugin warnings and adds a dated log.md entry for each durable change.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly bundle check (schedule; Claude Code routine; `0 7 * * 1`)
- **Verification:** okf lint is clean. Hard checks: every concept has frontmatter with a non-empty type; provenance timestamps carry a UTC offset; okf plugin audit shows no new warnings; no .mdx files in the bundle. On fail: notify, max 1 retries.
- **Memory:** bundle log.md at `log.md`. Read first: the newest log.md entries and the root index.md.

## Steps

1. **Start at the index.** The agent opens the nearest index.md and the latest log.md entries.
2. **Check structure.** It checks reserved files, lowercase names, links and that no .mdx is used.
3. **Check frontmatter.** It confirms each concept has a type and that provenance dates have an explicit UTC offset.
4. **Read the contracts.** It reads the generated .ok/okf/*.schema.json files instead of guessing field rules.
5. **Fix truthfully.** It corrects metadata without inventing facts, sources or verification.
6. **Log the change.** It adds a dated, newest-first log.md entry for each durable change.

Stop rule: Stops after 20 concepts and one retry per run.

## Permissions

- Writes: bundle .md files, log.md
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly bundle check. Verification: okf lint is clean. Memory: log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
