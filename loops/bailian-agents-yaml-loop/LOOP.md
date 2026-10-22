---
name: bailian-managed-agent
title: Bailian Managed Agent skill
repo: modelstudioai/cli
license: Apache-2.0
url: https://gethabit.dev/skills/modelstudioai/bailian-managed-agent
---

# Bailian Managed Agent skill

The bailian managed agent skill lets an agent manage hosted agents on Alibaba Cloud Bailian as code with bl managed-agent: init, validate, plan, apply and destroy from agents.yaml, plus sessions, files and memory stores. For teams who run managed agents.

- Install the skill: `npx skills add modelstudioai/cli --skill bailian-managed-agent`
- Source: https://github.com/modelstudioai/cli/tree/HEAD/skills/bailian-managed-agent
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You create a hosted Bailian agent; You preview agents.yaml changes; You manage sessions or memory stores.
Skip it when: You call an already published app; You manage your local agent's memory.

# Make it a habit: Agent infra changes stay reviewed.

When agents.yaml changes, your agent runs bl managed-agent validate and plan, shows you the diff and applies it only after your explicit yes. It never adds --yes by itself. A run log keeps each plan and apply result.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** agents.yaml changed (event; GitHub Actions or Claude Code routine; `push that changes agents.yaml`)
- **Verification:** validate, plan, your yes. Hard checks: bl managed-agent validate passes; bl managed-agent plan shows a diff before apply; apply runs with --yes only after confirmation. On fail: stop, max 0 retries.
- **Memory:** plan and apply log at `loops/bailian-agents-yaml-loop/runs.md`. Read first: the last applied plan and any failed creates.

## Steps

1. **Read the protocol.** The agent reads the shared bailian-protocol file for the high-risk confirmation rules.
2. **Validate.** It runs bl managed-agent validate, which works offline.
3. **Plan.** It runs bl managed-agent plan and shows you the pending diff.
4. **Wait for your yes.** It asks for explicit confirmation and stops if you decline or do not answer.
5. **Apply.** After your yes it runs bl managed-agent apply --yes.
6. **Log.** It writes the plan and the apply result to the log.

Stop rule: Stops after one agents.yaml change and one apply per run.

## Permissions

- Writes: loops/bailian-agents-yaml-loop/**, agents.yaml
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/bailian-agents-yaml-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: agents.yaml changed. Verification: validate, plan, your yes. Memory: loops/bailian-agents-yaml-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
