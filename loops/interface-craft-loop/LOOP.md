---
name: interface-design
title: Interface Design skill
repo: Dammyjay93/interface-design
license: MIT
url: https://gethabit.dev/skills/dammyjay93/interface-design
---

# Interface Design skill

The interface design skill helps agents build and review product UI such as dashboards, admin panels and SaaS tools with clear hierarchy, tokens, states and a saved design system.

- Install the skill: `npx skills add Dammyjay93/interface-design --skill interface-design`
- Source: https://github.com/Dammyjay93/interface-design/tree/HEAD/.claude/skills/interface-design
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You build a dashboard or admin panel; Your UI looks generic and flat; You want a design system kept across sessions.
Skip it when: You build a marketing or landing page; The work is brand-only.

# Make it a habit: Product UI that holds its system.

When a pull request changes product UI, your agent reads .interface-design/system.md, checks the change against its tokens, spacing and depth, runs the build and the four craft tests, and saves new reusable patterns back to system.md.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR changes product UI (event; Claude Code routine or GitHub Actions; `pull_request on UI component and style files`)
- **Verification:** build + craft tests. Hard checks: build, typecheck and tests pass; no hardcoded colors where semantic tokens exist; spacing values sit on the declared base unit; interactive elements have hover, focus and disabled states. Critic: claude-opus-5-5, pass at 17/20. On fail: retry, max 2 retries.
- **Memory:** design system file at `.interface-design/system.md`. Read first: direction, depth strategy, spacing unit and saved component patterns.

## Steps

1. **Read the system.** The agent reads .interface-design/system.md and the existing tokens and components.
2. **Explore if new.** Without a system file it lists domain, color world, signature and defaults, then asks if the direction feels right.
3. **State the checkpoint.** Before each component it writes intent, hierarchy, palette, depth, surfaces, typography and spacing.
4. **Use what exists.** It prefers native HTML, then a headless primitive, then the project's own components and tokens.
5. **Build and verify.** It runs build, typecheck and tests, then checks the screen at desktop and mobile widths.
6. **Craft tests.** Swap, squint, signature and token tests must pass before showing the result.
7. **Save patterns.** It offers to save new reusable patterns to system.md, and writes them when you say yes.

Stop rule: One pull request per run, at most two rework rounds on failed checks.

## Permissions

- Writes: UI files in the pull request, .interface-design/system.md
- Network: none
- Sends: nothing
- Human approval before anything ships: yes

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`.interface-design/system.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR changes product UI. Verification: build + craft tests. Memory: .interface-design/system.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
