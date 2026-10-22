---
name: index-knowledge
title: Index Knowledge skill
repo: tursodatabase/turso
license: MIT
url: https://gethabit.dev/skills/tursodatabase/index-knowledge
---

# Index Knowledge skill

The index knowledge skill generates a hierarchy of AGENTS.md files for a codebase: a root file plus files for complex subdirectories, picked by a scoring matrix and written by parallel agents. For teams onboarding coding agents.

- Install the skill: `npx skills add tursodatabase/turso --skill index-knowledge`
- Source: https://github.com/tursodatabase/turso/tree/HEAD/.claude/skills/index-knowledge
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: a repo has no AGENTS.md yet; AGENTS.md files are stale; onboarding agents to a large codebase.
Skip it when: the project has only a few files; you want hand-written docs only.

# Make it a habit: Agent docs match the codebase.

Each week your agent runs index-knowledge in update mode: parallel explore agents and a codemap score every directory, then root and subdirectory AGENTS.md files are updated, trimmed and deduplicated. Git history keeps each refresh.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly docs refresh (schedule; Claude Code routine; `0 6 * * 1`)
- **Verification:** size and dedupe checks. Hard checks: root AGENTS.md exists; root AGENTS.md is 50 to 150 lines; each subdirectory AGENTS.md is 30 to 80 lines; no child AGENTS.md repeats its parent; only directories scoring above 15, or 8 to 15 with a distinct domain, get a file. On fail: retry, max 1 retries.
- **Memory:** AGENTS.md commit history at `AGENTS.md`. Read first: existing AGENTS.md files and their key insights.

## Steps

1. **Plan the phases.** Your agent tracks discovery, scoring, generation and review with TodoWrite.
2. **Discover in parallel.** It launches explore agents scaled to project size and reads existing AGENTS.md and CLAUDE.md files.
3. **Map the code.** It measures structure with find and uses LSP symbols when available.
4. **Score directories.** It weights file count, subdirs, exports and references to pick AGENTS.md locations.
5. **Generate files.** It writes the root file first, then subdirectory files in parallel.
6. **Review and trim.** It removes generic advice and parent duplicates and prints the final report.

Stop rule: Stops after one pass over the repository, with max depth from --max-depth.

## Permissions

- Writes: **/AGENTS.md
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`AGENTS.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly docs refresh. Verification: size and dedupe checks. Memory: AGENTS.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
