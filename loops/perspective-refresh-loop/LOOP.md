---
name: huashu-nuwa
title: Huashu Nuwa skill
repo: alchaincyf/nuwa-skill
license: MIT
url: https://gethabit.dev/skills/alchaincyf/huashu-nuwa
---

# Huashu Nuwa skill

The huashu nuwa skill researches a public figure or a topic and distills how they think into a runnable perspective skill: mental models, decision rules, voice, values and honest limits.

- Install the skill: `npx skills add alchaincyf/nuwa-skill --skill huashu-nuwa`
- Source: https://github.com/alchaincyf/nuwa-skill
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You want a thinking advisor in someone's style; You have books or transcripts to distill; You want to refresh an existing perspective skill.
Skip it when: The person is private and has not agreed; You only need quotes, not a way of thinking.

# Make it a habit: Perspective skills stay current.

On a schedule, your agent picks a perspective skill made by huashu-nuwa, reads its research date, reruns only the conversation, decision and timeline research and adds new findings. quality_check.py must pass and you confirm the changes before they count.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** monthly perspective refresh (schedule; Claude Code routine; `0 8 1 * *`)
- **Verification:** quality check + your OK. Hard checks: quality_check.py reports PASS on all six items; 3 to 7 mental models, each with evidence; at least 3 honest limits and 2 tensions; research files saved under references/research/. On fail: retry, max 2 retries.
- **Memory:** research files at `.claude/skills/[person-name]-perspective/references/research/`. Read first: the research date in the honest-limits section and the 01-06 research files.

## Steps

1. **Pick the skill.** The agent picks a perspective skill under .claude/skills/ and reads its research date.
2. **Rerun three agents.** Only the conversation, decision and timeline research run again and save to 02, 05 and 06 files.
3. **Compare.** New facts add cases, mark changed views or suggest a new model.
4. **Update in place.** It updates the latest-news section and research date without rewriting the skill.
5. **Quality check.** It runs quality_check.py on the SKILL.md and fixes failing items.
6. **Confirm with you.** It shows a change summary and waits for your OK.

Stop rule: One perspective skill per run, at most two fix rounds, then ship with weak areas marked.

## Permissions

- Writes: .claude/skills/**
- Network: web search, github.com
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`.claude/skills/[person-name]-perspective/references/research/`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: monthly perspective refresh. Verification: quality check + your OK. Memory: .claude/skills/[person-name]-perspective/references/research/. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
