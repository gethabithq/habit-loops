---
name: better-colors
title: Better Colors skill
repo: jakubkrehel/skills
license: MIT
url: https://gethabit.dev/skills/jakubkrehel/better-colors
---

# Better Colors skill

The better colors skill builds and audits color systems: ramps, semantic token names, format conversion and measured contrast, reported by severity. For frontend and design teams who keep a token-based palette.

- Install the skill: `npx skills add jakubkrehel/skills --skill better-colors`
- Source: https://github.com/jakubkrehel/skills/tree/HEAD/skills/better-colors
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You build a new color palette; You review token use in a PR; You check text contrast.
Skip it when: You need shadow or icon color rules; You only pick one brand color.

# Make it a habit: Color tokens stay used by role.

On each pull request that touches styles, your agent runs better colors: it checks for raw color literals, primitives used in components, tokens used outside their role and measured contrast pairs. It ends with Block or Approve and logs findings.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR touches styles (event; GitHub Actions or Claude Code routine; `pull_request paths: **/*.css, **/*.tsx`)
- **Verification:** no HIGH color findings. Hard checks: no hex, rgb or oklch literal in a component where a token exists; every reported contrast value was measured; count of HIGH findings is zero for Approve. On fail: notify, max 0 retries.
- **Memory:** color findings log at `loops/color-system-audit-loop/findings.md`. Read first: project notation, token tiers and open findings.

## Steps

1. **Learn the system.** Read the project's tokens and notation and match them.
2. **Check tiers.** Flag primitives like var(--blue-600) used directly in components.
3. **Check roles.** Flag tokens used outside their role, such as a border token in color.
4. **Check ramps.** Look for hue drift, uneven light steps and copied chroma.
5. **Measure pairs.** Measure each rendered text pair in light and dark and report failures.
6. **Report.** Write one row per root cause by severity and end with Block or Approve.

Stop rule: Stops after one pull request per run.

## Permissions

- Writes: loops/color-system-audit-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/color-system-audit-loop/findings.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR touches styles. Verification: no HIGH color findings. Memory: loops/color-system-audit-loop/findings.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
