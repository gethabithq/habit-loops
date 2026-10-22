---
name: xiaohongshu
title: Xiaohongshu skill
repo: autoclaw-cc/xiaohongshu-mcp-skills
license: MIT
url: https://gethabit.dev/skills/autoclaw-cc/xiaohongshu
---

# Xiaohongshu skill

The xiaohongshu skill automates Xiaohongshu (RED) through xiaohongshu-mcp: login, posting notes and videos, searching, browsing, liking and commenting, creator profiles and content planning. For people running Xiaohongshu accounts.

- Install the skill: `npx skills add autoclaw-cc/xiaohongshu-mcp-skills --skill xiaohongshu`
- Source: https://github.com/autoclaw-cc/xiaohongshu-mcp-skills
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: posting a Xiaohongshu note; searching Xiaohongshu notes; planning Xiaohongshu content.
Skip it when: xiaohongshu-mcp is not set up; you want no automated public actions.

# Make it a habit: Notes planned and posted with approval.

On a schedule, your agent checks the xiaohongshu-mcp tools and login, searches notes and creator profiles for your topics, drafts a content plan, and posts or comments only after you confirm each item. A plan file keeps topics and drafts.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly content planning (schedule; Claude Code routine; `0 9 * * 1`)
- **Verification:** tools ready, you approve. Hard checks: check_login_status is available and reports logged in; feed_id and xsec_token come from search or browse results; no post or comment goes out without your confirmation. On fail: stop, max 0 retries.
- **Memory:** content plan file at `loops/xhs-content-plan-loop/plan.md`. Read first: past topics, drafts and what was already posted.

## Steps

1. **Check tools.** Your agent checks that check_login_status exists, or tells you to run /setup-xhs-mcp.
2. **Check login.** It confirms the login state before any other tool.
3. **Research.** It searches notes and views creator profiles for your topics.
4. **Plan.** It drafts topics and notes with the content-planning sub-skill.
5. **Confirm.** It shows each post or comment and waits for your yes.
6. **Publish.** It publishes only the items you approved.

Stop rule: Stops after one planning pass per run; nothing is published without your confirmation.

## Permissions

- Writes: loops/xhs-content-plan-loop/**
- Network: none
- Sends: approved notes and comments on Xiaohongshu
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/xhs-content-plan-loop/plan.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly content planning. Verification: tools ready, you approve. Memory: loops/xhs-content-plan-loop/plan.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
