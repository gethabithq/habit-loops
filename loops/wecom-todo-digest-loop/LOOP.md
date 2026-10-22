---
name: wecomcli-todo
title: WeCom CLI Todo skill
repo: WecomTeam/wecom-cli
license: MIT
url: https://gethabit.dev/skills/wecomteam/wecomcli-todo
---

# WeCom CLI Todo skill

The wecom cli todo skill lets agents create, list, finish, update and delete WeCom todos through wecom-cli, including deadlines and reminders, for teams on WeCom.

- Install the skill: `npx skills add WecomTeam/wecom-cli --skill wecomcli-todo`
- Source: https://github.com/WecomTeam/wecom-cli/tree/HEAD/skills/wecomcli-todo
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You want to see your open WeCom todos; You create a todo with a deadline; You update or finish a todo.
Skip it when: Your team does not use WeCom; You need calendar events.

# Make it a habit: Open todos reviewed every morning.

Every workday morning your agent lists your unfinished WeCom todos with wecom-cli, sorts them by deadline, shows what is due soon and keeps a log so the next run can spot todos that keep slipping.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** workday morning digest (schedule; Claude Code routine or cron; `0 8 * * 1-5`)
- **Verification:** list call succeeds. Hard checks: the wecomcli-shared pre-check passes before any wecom-cli command; todo list returns without an error; no todo_id appears in the digest shown to you. On fail: notify, max 1 retries.
- **Memory:** open todo log at `loops/wecom-todo-digest-loop/run-log.md`. Read first: todos open in the last run and their deadlines.

## Steps

1. **Run pre-check.** The agent first completes the shared checks from the wecomcli-shared skill.
2. **Read the reference.** It reads references/todo-list.md fully before building the command.
3. **List open todos.** It runs todo list filtered to unfinished todos.
4. **Sort by deadline.** It orders them by the deadline object, with date and datetime types handled.
5. **Compare.** It flags todos that were already open in the last run's log.
6. **Show and log.** It shows you the digest without todo IDs and writes the list to the log.

Stop rule: Stops after one digest per run, with at most one retry of the list call.

## Permissions

- Writes: loops/wecom-todo-digest-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/wecom-todo-digest-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: workday morning digest. Verification: list call succeeds. Memory: loops/wecom-todo-digest-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
