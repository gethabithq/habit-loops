---
name: paperclip-create-agent
title: Paperclip Create Agent skill
repo: paperclipai/paperclip
license: MIT
url: https://gethabit.dev/skills/paperclipai/paperclip-create-agent
---

# Paperclip Create Agent skill

Paperclip create agent guides an agent through hiring a new agent in Paperclip: permission checks, adapter discovery, a drafted config, a review checklist, the hire request and the board approval follow-up. For Paperclip operators.

- Install the skill: `npx skills add paperclipai/paperclip --skill paperclip-create-agent`
- Source: https://github.com/paperclipai/paperclip/tree/HEAD/skills/paperclip-create-agent
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You must hire a new agent; You compare adapter configs; You follow a pending hire approval.
Skip it when: You lack hiring permission; You need only a temporary subagent.

# Make it a habit: A reviewed hire request, submitted.

When a hire is requested in Paperclip, your agent checks its hiring permission, studies adapter options and existing configs, drafts the new agent, walks the draft-review checklist and submits it. Then it follows the approval and closes linked issues.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** hire task assigned (event; Paperclip Runner or Claude Code routine; `task asks to hire or create an agent`)
- **Verification:** checklist plus board approval. Hard checks: every item in draft-review-checklist.md passes; the agent-hires request returns without an error; the draft has an icon from /llms/agent-icons.txt. On fail: notify, max 0 retries.
- **Memory:** hire log at `loops/paperclip-hire-loop/hires.md`. Read first: pending approvals and their linked issues.

## Steps

1. **Check permission.** Confirm board access or can_create_agents=true; if missing, leave a human-input request and stop.
2. **Learn the setup.** Read /api/agents/me, the agent-configuration files and existing agent configurations.
3. **Describe the role.** Write a short role paragraph using the baseline role guide or role examples.
4. **Draft the config.** Set name, icon, reportsTo, adapter type, desiredSkills and capabilities, with heartbeats off by default.
5. **Review the draft.** Walk the draft-review checklist and fix every item that fails.
6. **Submit.** Post the hire to the agent-hires endpoint.
7. **Follow approval.** On approval, read linked issues and close them or comment with next steps.

Stop rule: Stops after one hire request per run; a denied permission ends the run.

## Permissions

- Writes: loops/paperclip-hire-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/paperclip-hire-loop/hires.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: hire task assigned. Verification: checklist plus board approval. Memory: loops/paperclip-hire-loop/hires.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
