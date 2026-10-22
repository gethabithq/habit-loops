---
name: linkedin-marketing
title: LinkedIn Marketing skill
repo: sergebulaev/linkedin-skills
license: MIT
url: https://gethabit.dev/skills/sergebulaev/linkedin-marketing
---

# LinkedIn Marketing skill

Linkedin marketing is a bundle of skills for creators and founders who plan, draft, audit and publish LinkedIn posts and comments, with voice rules, hook formulas and an approval step before anything goes live.

- Install the skill: `npx skills add sergebulaev/linkedin-skills --skill linkedin-marketing`
- Source: https://github.com/sergebulaev/linkedin-skills
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You plan a week of LinkedIn posts; You draft a comment on a post; You want AI tells removed.
Skip it when: You do not post on LinkedIn; You want posts sent without review.

# Make it a habit: A week of posts, approved first.

Every Monday, your agent plans the week with linkedin-content-planner, drafts posts with linkedin-post-writer, audits each with linkedin-humanizer and waits for your approval. Only approved drafts are published through Publora or handed over to paste.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** every Monday morning (schedule; Claude Code routine; `0 8 * * 1`)
- **Verification:** audit and your approval. Hard checks: each post is 900 to 1,300 characters; the hook sits in the first 210 characters; no listed AI word such as leverage or delve appears; nothing is published without your yes. On fail: retry, max 2 retries.
- **Memory:** story bank at `references/story-bank.md`. Read first: your story bank answers and last week's plan.

## Steps

1. **Check the story bank.** Read references/story-bank.md, and run linkedin-interviewer if there is nothing concrete to write about.
2. **Plan the week.** Use linkedin-content-planner, asking founder plan or general plan.
3. **Draft posts.** Write each planned post with linkedin-post-writer and the hook formulas.
4. **Audit drafts.** Run linkedin-humanizer in --mode audit to remove AI tells and check voice rules.
5. **Wait for approval.** Show each draft and wait for the user to say post or yes.
6. **Publish or hand over.** Publish approved posts through the Publora API, or return a copy-paste block.

Stop rule: Stops after five drafted posts per week and two rewrites per post.

## Permissions

- Writes: references/story-bank.md, loops/linkedin-weekly-content-loop/**
- Network: publora.com
- Sends: LinkedIn posts via Publora, only after your approval
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`references/story-bank.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: every Monday morning. Verification: audit and your approval. Memory: references/story-bank.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
