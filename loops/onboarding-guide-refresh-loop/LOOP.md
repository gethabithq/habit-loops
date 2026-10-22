---
name: understand-onboard
title: Understand Onboard skill
repo: egonex-ai/understand-anything
license: MIT
url: https://gethabit.dev/skills/egonex-ai/understand-onboard
---

# Understand Onboard skill

Understand onboard turns a codebase knowledge graph into an onboarding guide with overview, architecture layers, key concepts, a guided tour, a file map and complexity hotspots. For teams bringing new developers onto a project.

- Install the skill: `npx skills add egonex-ai/understand-anything --skill understand-onboard`
- Source: https://github.com/egonex-ai/understand-anything/tree/HEAD/understand-anything-plugin/skills/understand-onboard
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: a new team member joins; the architecture changed a lot; docs lack a project overview.
Skip it when: no knowledge graph exists yet; you need function-level detail.

# Make it a habit: Onboarding guide matches the code.

After the knowledge graph is refreshed, your agent rebuilds the onboarding guide from its project data, layers, tour and file nodes, flags complexity hotspots and offers to save it to docs/UA_ONBOARDING.md. You approve the save and commit.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** graph refreshed (event; Claude Code routine; `knowledge-graph.json updated by /understand`)
- **Verification:** sections check, you approve. Hard checks: knowledge-graph.json exists in the data directory; guide has all six sections; git diff since the graph commit lists no project files, or a stale warning is shown. On fail: notify, max 0 retries.
- **Memory:** guide history in git at `docs/UA_ONBOARDING.md`. Read first: the last committed onboarding guide.

## Steps

1. **Find the graph.** Resolve .ua or the older .understand-anything and stop with a hint to run /understand if no graph exists.
2. **Check freshness.** Compare the graph commit with HEAD and the project diff and warn if files changed.
3. **Read structure.** Read the project section, layers, tour and only file-level nodes.
4. **Find hotspots.** Pick the file nodes with the highest complexity values.
5. **Write the guide.** Build overview, layers, key concepts, guided tour, file map and hotspots in Markdown.
6. **Save on approval.** Ask you before saving to docs/UA_ONBOARDING.md and suggest a commit.

Stop rule: Stops after one guide per run.

## Permissions

- Writes: docs/UA_ONBOARDING.md
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`docs/UA_ONBOARDING.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: graph refreshed. Verification: sections check, you approve. Memory: docs/UA_ONBOARDING.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
