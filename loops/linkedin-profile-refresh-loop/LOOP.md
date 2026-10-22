---
name: linkedin-profile-optimizer
title: LinkedIn Profile Optimizer skill
repo: paramchoudhary/resumeskills
license: MIT
url: https://gethabit.dev/skills/paramchoudhary/linkedin-profile-optimizer
---

# LinkedIn Profile Optimizer skill

The linkedin profile optimizer skill rewrites your headline, About and experience sections with recruiter keywords and scores profile completeness, for job seekers who want more recruiter visibility.

- Install the skill: `npx skills add paramchoudhary/resumeskills --skill linkedin-profile-optimizer`
- Source: https://github.com/paramchoudhary/resumeskills/tree/HEAD/.agents/skills/linkedin-profile-optimizer
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You start a job search; Your headline is only a job title; You want LinkedIn to match your resume.
Skip it when: You need a full resume rewrite; You want posts written for you.

# Make it a habit: Your profile stays search ready.

Once a month your agent compares your saved LinkedIn profile text with your resume and target roles, rewrites headline and About within the character limits, scores completeness against the checklist and keeps the scores so you see progress.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** first day each month (schedule; Claude Code routine; `0 9 1 * *`)
- **Verification:** limits and sections check. Hard checks: headline is at most 220 characters; About section is at most 2,600 characters; report contains assessment, optimized sections and action items; completeness score is filled in. On fail: retry, max 1 retries.
- **Memory:** profile score history at `loops/linkedin-profile-refresh-loop/history.md`. Read first: last completeness and searchability scores and open action items.

## Steps

1. **Load the inputs.** Read the saved profile text, the resume and the target roles, plus the last entry in the history file.
2. **Assess the profile.** Score completeness and searchability, and list key issues against the All-Star checklist.
3. **Rewrite the headline.** Build a new headline from role, key expertise and value with keywords recruiters search for.
4. **Rewrite About.** Draft a hook, three short paragraphs, a skills list and a call to action within the limit.
5. **Improve experience and skills.** Suggest additions and changes per role, skills to add and keywords to place.
6. **Write action items.** Output the report in the skill's format and append the scores and open items to the history file.

Stop rule: Stops after one profile report per run, with at most one rewrite after a failed check.

## Permissions

- Writes: loops/linkedin-profile-refresh-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/linkedin-profile-refresh-loop/history.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: first day each month. Verification: limits and sections check. Memory: loops/linkedin-profile-refresh-loop/history.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
