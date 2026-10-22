---
name: n8n-workflow-lifecycle-official
title: n8n Workflow Lifecycle skill
repo: n8n-io/skills
license: Apache-2.0
url: https://gethabit.dev/skills/n8n-io/n8n-workflow-lifecycle-official
---

# n8n Workflow Lifecycle skill

The n8n workflow lifecycle skill helps automation builders plan, build, validate, test, publish and hand off n8n workflows, with naming, node groups, sticky notes and folders done right.

- Install the skill: `npx skills add n8n-io/skills --skill n8n-workflow-lifecycle-official`
- Source: https://github.com/n8n-io/skills/tree/HEAD/skills/n8n-workflow-lifecycle-official
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You build a new n8n workflow; You are about to publish a workflow; You organize workflows into folders.
Skip it when: You do not use n8n; You only need a single node edit.

# Make it a habit: n8n workflows shipped only after testing.

For every new or changed n8n workflow, your agent plans, builds, runs validate_workflow, checks connections with get_workflow_details, has you confirm credentials, tests with pinned data and only then publishes and writes a handoff. A log keeps handoffs.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** workflow request arrives (manual; Claude Code routine; `run when you ask for a new or changed n8n workflow`)
- **Verification:** validate, verify, test, then publish. Hard checks: validate_workflow passes; get_workflow_details connections match the intended wiring; test_workflow output matches intent on pinned data; no skippedGroups, skippedOperations or removedGroups left unrepaired. On fail: stop, max 1 retries.
- **Memory:** workflow handoff log at `loops/n8n-workflow-ship-loop/run-log.md`. Read first: handoff notes and naming used for nearby workflows.

## Steps

1. **Plan.** Clarify the request and search_workflows for existing workflows or sub-workflows that already do it.
2. **Build.** Write SDK code with create_workflow_from_code, a description and clear node names.
3. **Validate.** Run validate_workflow, then check connections with get_workflow_details.
4. **User wire-up.** Ask you to verify per-node credentials and create anything missing.
5. **Test.** Run test_workflow with prepare_workflow_pin_data, asking first if unpinned nodes have side effects.
6. **Publish.** Call publish_workflow only after validation and testing are clean.
7. **Hand off.** Write how it triggers, what it returns, how to invoke it and what to watch.

Stop rule: Stops after one workflow per run, with at most one fix round before asking you.

## Permissions

- Writes: loops/n8n-workflow-ship-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/n8n-workflow-ship-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: workflow request arrives. Verification: validate, verify, test, then publish. Memory: loops/n8n-workflow-ship-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
