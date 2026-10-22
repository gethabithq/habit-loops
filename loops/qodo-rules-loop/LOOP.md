---
name: qodo-get-rules
title: Qodo Get Rules skill
repo: qodo-ai/qodo-skills
license: MIT
url: https://gethabit.dev/skills/qodo-ai/qodo-get-rules
---

# Qodo Get Rules skill

The qodo get rules skill helps development teams retrieve their organization's Qodo coding rules for a task and apply them by severity while the agent writes or reviews code.

- Install the skill: `npx skills add qodo-ai/qodo-skills --skill qodo-get-rules`
- Source: https://github.com/qodo-ai/qodo-skills/tree/HEAD/antigravity-plugins/qodo-standards/skills/qodo-get-rules
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You start a concrete coding task; Your team keeps coding rules in Qodo; You review code against team standards.
Skip it when: You do not use Qodo; The task is too vague to query.

# Make it a habit: Team coding rules applied every task.

At the start of every coding task your agent reuses or retrieves the team's Qodo rules with two structured queries, merges them, explains what each means for the change and applies them. A rules file keeps results per scope for reuse.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** coding task starts (event; Claude Code routine; `a concrete implementation, refactor or review task begins`)
- **Verification:** rules loaded and applied. Hard checks: qodo --version is 1.6.0 or newer before any retrieval; two queries ran: topic and cross-cutting; merged list has no duplicate rule id; every ERROR rule is followed or the user approved a deviation. On fail: stop, max 0 retries.
- **Memory:** rules per scope at `loops/qodo-rules-loop/rules.md`. Read first: rules already retrieved for this workspace, repository and task scope.

## Steps

1. **Reuse first.** If saved rules still cover this scope, skip retrieval and apply them.
2. **Check runtime.** Run qodo --version, then qodo read whoami, or use the read-only rules-search MCP tool.
3. **Find the scope.** Take the repo path from the origin remote, or omit --scopes when none parses.
4. **Write two queries.** Build a topic query and a cross-cutting query in the Name, Category, Content format.
5. **Search and merge.** Run qodo read rules search with --top-k 20 for each, merge and dedup by id.
6. **Explain and apply.** Say what each rule means for the change and apply it by severity.
7. **Ask on ERROR.** If an ERROR rule must be broken, stop and ask the user.

Stop rule: Stops after one task; at most one broadened retry when a topic query returns fewer than 3 rules.

## Permissions

- Writes: loops/qodo-rules-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/qodo-rules-loop/rules.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: coding task starts. Verification: rules loaded and applied. Memory: loops/qodo-rules-loop/rules.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
