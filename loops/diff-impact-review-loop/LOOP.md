---
name: understand-diff
title: Understand Diff skill
repo: egonex-ai/understand-anything
license: MIT
url: https://gethabit.dev/skills/egonex-ai/understand-diff
---

# Understand Diff skill

Understand diff analyzes git diffs and pull requests against a codebase knowledge graph to show changed components, affected neighbours, touched layers and a risk rating. For reviewers who want to know what a change could break.

- Install the skill: `npx skills add egonex-ai/understand-anything --skill understand-diff`
- Source: https://github.com/egonex-ai/understand-anything/tree/HEAD/understand-anything-plugin/skills/understand-diff
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: reviewing a pull request; checking the blast radius of a change; seeing which layers a branch touches.
Skip it when: no knowledge graph exists yet; a one-line change.

# Make it a habit: Every PR gets an impact map.

On each pull request, your agent lists the changed files, checks the knowledge graph is fresh, finds the matching nodes and their one-hop neighbours, and writes changed parts, affected parts, layers and a risk rating. It saves diff-overlay.json for the dashboard.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** pull request opened (event; GitHub Actions or Claude Code routine; `pull_request opened or synchronize`)
- **Verification:** graph found, overlay written. Hard checks: knowledge-graph.json exists in the data directory; changed file list is not empty; diff-overlay.json is written with changedNodeIds and affectedNodeIds; stale graph warning shown when the project diff lists files. On fail: notify, max 0 retries.
- **Memory:** diff overlay file at `.ua/diff-overlay.json`. Read first: the last overlay's base branch and affected node ids.

## Steps

1. **Find the graph.** Resolve .ua or the older .understand-anything and stop with a hint to run /understand if no graph exists.
2. **List changes.** Get changed files with git diff --name-only or against the base branch.
3. **Check freshness.** Compare the graph commit with HEAD and the project diff and warn if the graph is stale.
4. **Map nodes.** Grep the graph for each changed filePath and note the node ids.
5. **Follow edges.** Find upstream and downstream nodes one hop away and the layers they sit in.
6. **Rate the risk.** Use complexity, cross-layer edges and blast radius to say what to review closely.
7. **Write the overlay.** Save diff-overlay.json so the dashboard can show the change.

Stop rule: Stops after one pull request per run.

## Permissions

- Writes: .ua/diff-overlay.json, .understand-anything/diff-overlay.json
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`.ua/diff-overlay.json`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: pull request opened. Verification: graph found, overlay written. Memory: .ua/diff-overlay.json. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
