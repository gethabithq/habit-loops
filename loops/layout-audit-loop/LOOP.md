---
name: better-layout
title: Better Layout skill
repo: jakubkrehel/skills
license: MIT
url: https://gethabit.dev/skills/jakubkrehel/better-layout
---

# Better Layout skill

The better layout skill reviews grouping, alignment, reading order and responsive structure, then stress-tests a layout for resizing, translated text and RTL mirroring.

- Install the skill: `npx skills add jakubkrehel/skills --skill better-layout`
- Source: https://github.com/jakubkrehel/skills/tree/HEAD/skills/better-layout
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: Your UI must support translated text; You ship RTL languages; Layouts clip on small screens or zoom.
Skip it when: You need an accessibility audit; The change is copy only.

# Make it a habit: Layouts survive resize, translation, RTL.

When a pull request changes layout or styles, your agent scans for the skill's detection patterns, checks grouping, order and logical properties, and tests 320px, 200% zoom and RTL where a browser exists. It ends with Block or Approve and logs root causes.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR changes styles (event; GitHub Actions or Claude Code routine; `pull_request on CSS, style and layout component files`)
- **Verification:** detection table, no HIGH. Hard checks: no detection-table pattern left, like width: 100vw or fixed height on text boxes; no clipping or overlap at 320px or 200% zoom; visual order matches DOM order; verdict is Approve, not Block. On fail: notify, max 0 retries.
- **Memory:** findings by root cause at `loops/layout-audit-loop/run-log.md`. Read first: open HIGH and MEDIUM findings and checks marked Not verified.

## Steps

1. **Scan patterns.** The agent checks the diff against the Before you finish detection table.
2. **Check structure.** It reviews grouping by space, shared edges, reading order and one primary action.
3. **Check mirroring.** It looks for physical left and right where logical inline properties belong.
4. **Stress test.** With a browser it tests every supported width, 320px, 200% zoom and the RTL mirror.
5. **Report.** Findings go in a severity table, one row per root cause, with checks not run marked Not verified.
6. **Verdict.** It ends with Block if any HIGH remains, otherwise Approve.

Stop rule: One pull request per run; the run stops at the verdict.

## Permissions

- Writes: loops/layout-audit-loop/**
- Network: api.github.com
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/layout-audit-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR changes styles. Verification: detection table, no HIGH. Memory: loops/layout-audit-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
