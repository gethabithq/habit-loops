---
name: better-typography
title: Better Typography skill
repo: jakubkrehel/skills
license: MIT
url: https://gethabit.dev/skills/jakubkrehel/better-typography
---

# Better Typography skill

The better typography skill sets and reviews how text renders: type scale, line-height, letter-spacing, font loading, wrapping, truncation, tabular numbers and punctuation. For frontend teams who want clean, readable text.

- Install the skill: `npx skills add jakubkrehel/skills --skill better-typography`
- Source: https://github.com/jakubkrehel/skills/tree/HEAD/skills/better-typography
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You review text styles in a PR; Text wraps or truncates badly; Numbers shift in timers or tables.
Skip it when: You need copywriting help; You are choosing a brand typeface.

# Make it a habit: Text renders right on every PR.

On each pull request that touches styles, your agent runs better typography: it checks line-height units, weights, measure, tabular numbers, wrapping, truncation and 16px mobile inputs against the pattern table, then ends with Block or Approve.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR touches styles (event; GitHub Actions or Claude Code routine; `pull_request paths: **/*.css, **/*.tsx`)
- **Verification:** no HIGH findings left. Hard checks: no line-height in px or rem; no weight 100 to 300 on text under 18px; count of HIGH findings is zero for Approve. On fail: notify, max 0 retries.
- **Memory:** type findings log at `loops/typography-review-loop/findings.md`. Read first: the project's type scale and open findings.

## Steps

1. **Read the scale.** Find the project's type scale and judge against it.
2. **Check measured rules.** Check unitless line-height, weights, measure, tabular-nums and 16px inputs.
3. **Check wrapping.** Check balance, pretty, truncation and a way back to full text.
4. **Check fonts.** Make sure loaded faces match the weights used and properties replace raw tags.
5. **Hand off.** Leave words, headings structure, layout and contrast to the sibling better skills.
6. **Report.** Write one row per root cause by severity and end with Block or Approve.

Stop rule: Stops after one pull request per run.

## Permissions

- Writes: loops/typography-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/typography-review-loop/findings.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR touches styles. Verification: no HIGH findings left. Memory: loops/typography-review-loop/findings.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
