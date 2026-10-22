---
name: brief
title: Content Brief skill
repo: calm-north/seojuice-skills
license: MIT
url: https://gethabit.dev/skills/calm-north/brief
---

# Content Brief skill

The content brief skill produces an editor-ready SEO content brief for a keyword: SERP review, intent mapping, titles, meta description, outline, E-E-A-T requirements, SEO targets and a differentiation angle. For content teams and SEO writers.

- Install the skill: `npx skills add calm-north/seojuice-skills --skill brief`
- Source: https://github.com/calm-north/seojuice-skills/tree/HEAD/skills/brief
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You need an SEO content brief; You outline a blog post for a keyword; You brief a freelance writer.
Skip it when: You still need to pick keywords; You want a full site audit.

# Make it a habit: One editor-ready brief per keyword.

Each week your agent takes the next keyword from your queue, reviews the top results, maps intent, writes title options, meta description and heading outline, sets E-E-A-T and SEO targets and picks a differentiation angle. A board tracks briefs done.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** weekly brief batch (schedule; Claude Code routine; `0 9 * * 3`)
- **Verification:** brief completeness check. Hard checks: titles are under 60 characters and include the keyword; meta description is 150 to 160 characters; brief has SERP table, outline, SEO targets and E-E-A-T checklist; 1 or 2 differentiation angles chosen. On fail: retry, max 1 retries.
- **Memory:** keyword brief board at `loops/content-brief-queue-loop/board.md`. Read first: next keywords in the queue and briefs already written.

## Steps

1. **Gather context.** Your agent confirms keyword, business goal, content type and audience.
2. **Analyze results.** It searches the keyword and records format, length and angle of the top 5 to 10.
3. **Map intent.** It matches structure to how-to, what-is, best-of, versus or review intent.
4. **Outline.** It writes 2 to 3 titles, a meta description and every H2 and H3 with guidance.
5. **Set E-E-A-T.** It runs the YMYL check and sets author and evidence requirements.
6. **Set targets.** It sets SEO targets and picks 1 or 2 angles to beat current results.

Stop rule: Stops after 3 briefs per run.

## Permissions

- Writes: loops/content-brief-queue-loop/**
- Network: seojuice.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/content-brief-queue-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: weekly brief batch. Verification: brief completeness check. Memory: loops/content-brief-queue-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
