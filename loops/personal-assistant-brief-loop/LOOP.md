---
name: personal-assistant
title: Personal Assistant skill
repo: ailabs-393/ai-labs-claude-skills
license: MIT
url: https://gethabit.dev/skills/ailabs-393/personal-assistant
---

# Personal Assistant skill

The personal assistant skill keeps a local profile of your schedule, goals, habits and tasks, and uses it for task tracking, reminders, schedule conflicts and productivity advice tailored to you.

- Install the skill: `npx skills add ailabs-393/ai-labs-claude-skills --skill personal-assistant`
- Source: https://github.com/ailabs-393/ai-labs-claude-skills/tree/HEAD/dist/skills/personal-assistant
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You want a daily task plan; You track goals and habits; You need schedule conflict checks.
Skip it when: You need real calendar sync; You do not want a stored profile.

# Make it a habit: A daily plan from your profile.

Each morning your agent loads your profile, tasks, schedule and context, lists today's and overdue tasks, flags clashes and suggests a plan that fits your goals. Once a month it runs cleanup. Your data stays in the skill's own files.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every weekday morning (schedule; Claude Code routine; `0 7 * * 1-5`)
- **Verification:** profile loaded, you confirm. Hard checks: assistant_db.py has_profile returns true; task_helper.py today and overdue run without error; brief lists every overdue task. On fail: notify, max 0 retries.
- **Memory:** assistant profile and tasks at `~/.claude/personal_assistant/`. Read first: profile.json, tasks.json, schedule.json and context.json.

## Steps

1. **Check the profile.** Run assistant_db.py has_profile; if false, ask the setup questions and save the profile.
2. **Load the context.** Read profile, tasks, schedule and context with assistant_db.py.
3. **List today's work.** Run task_helper.py today and overdue.
4. **Flag conflicts.** Compare new items with recurring commitments and working hours.
5. **Suggest the plan.** Order tasks by goals and working style, and ask before adding events.
6. **Record the context.** Add the interaction with add_context and run cleanup once a month.

Stop rule: Stops after one brief per day.

## Permissions

- Writes: ~/.claude/personal_assistant/**
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`~/.claude/personal_assistant/`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every weekday morning. Verification: profile loaded, you confirm. Memory: ~/.claude/personal_assistant/. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
