---
name: resume-tailor
title: Resume Tailor skill
repo: paramchoudhary/resumeskills
license: MIT
url: https://gethabit.dev/skills/paramchoudhary/resume-tailor
---

# Resume Tailor skill

The resume tailor skill adapts your master resume to one job posting: it rewrites the summary, reorders skills and bullets and adds keywords without inventing anything. For job seekers who apply to many roles.

- Install the skill: `npx skills add paramchoudhary/resumeskills --skill resume-tailor`
- Source: https://github.com/paramchoudhary/resumeskills/tree/HEAD/skills/resume-tailor
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You apply to a specific job posting; Your resume is too generic; You keep several targeted versions.
Skip it when: You have no master resume yet; You want to write a resume from scratch.

# Make it a habit: A truthful resume per posting.

Each time you add a job posting, your agent runs the job description analyzer, then tailors your master resume to that role. A checklist check confirms title, top skills and unchanged metrics, and a board tracks which version went to which company.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** new job posting added (event; Claude Code routine; `a new job description is added to the loop folder`)
- **Verification:** tailoring checklist passes. Hard checks: summary names the exact job title from the posting; top 5 skills match the posting's top 5 requirements; no numbers or metrics differ from the master resume; keywords added count is above zero. On fail: retry, max 1 retries.
- **Memory:** versions per company at `loops/resume-tailor-loop/board.md`. Read first: which tailored version went to which company and the saved tailoring notes.

## Steps

1. **Analyze the posting.** Run the job-description-analyzer skill first to get required skills, keywords and priorities.
2. **Audit the resume.** Go through each section of the master resume and judge how well it fits this role.
3. **Rewrite the summary.** Reshape the professional summary so it mirrors the main needs of the posting.
4. **Reorder skills and experience.** Move the most relevant skills, jobs and bullets to the top and weave keywords in truthfully.
5. **Write the change report.** Produce the tailored resume changes report with before and after for each section.
6. **Run the checklist.** Check the quick tailoring checklist, including truthful claims and ATS formatting, then log the version.

Stop rule: One job posting per run; one retry if the checklist fails, then stop.

## Permissions

- Writes: loops/resume-tailor-loop/
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/resume-tailor-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: new job posting added. Verification: tailoring checklist passes. Memory: loops/resume-tailor-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
