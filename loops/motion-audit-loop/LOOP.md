---
name: design-motion-principles
title: Design Motion Principles skill
repo: kylezantos/design-motion-principles
license: MIT
url: https://gethabit.dev/skills/kylezantos/design-motion-principles
---

# Design Motion Principles skill

The design motion principles skill helps front-end developers build purposeful UI animations or audit existing ones, with context-weighted design lenses, a frequency gate and an HTML report.

- Install the skill: `npx skills add kylezantos/design-motion-principles --skill design-motion-principles`
- Source: https://github.com/kylezantos/design-motion-principles/tree/HEAD/skills/design-motion-principles
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You add transitions or hover states; You review animations in a pull request; Motion feels generic or too loud.
Skip it when: Your project has no UI motion; You need game engine or video animation.

# Make it a habit: Motion reviewed on every UI change.

When a pull request changes UI animations, your agent runs design motion principles in Audit mode, weights the three lenses by project type, checks reduced motion support and writes the HTML report. A log keeps past findings.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR touches UI motion (event; GitHub Actions or Claude Code routine; `pull_request.opened or synchronize, paths: CSS, React or Framer Motion files`)
- **Verification:** reduced motion and report. Hard checks: every changed animation handles prefers-reduced-motion; the HTML audit report file exists; every finding is checked against the anti-checklist. On fail: notify, max 0 retries.
- **Memory:** motion audit log at `loops/motion-audit-loop/log.md`. Read first: project type, chosen lens weights and open findings from past audits.

## Steps

1. **Pick up change.** A pull request that changes animations starts the run, so the mode is Audit.
2. **Weight the lenses.** The agent reads the project type and picks primary, secondary and selective lenses from the mapping table.
3. **Apply frequency gate.** Each animation is judged by how often a user triggers it, and keyboard actions should not animate.
4. **Run the checklists.** The agent follows workflows/audit.md with the audit checklist, the anti-checklist and the accessibility reference.
5. **Write the report.** Findings go into the HTML report with demo cards, as the output format reference describes.
6. **Log the run.** Lens weights and open findings go into the log for the next audit.

Stop rule: Stops after one pull request per run, with at most 20 animations reviewed.

## Permissions

- Writes: loops/motion-audit-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/motion-audit-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR touches UI motion. Verification: reduced motion and report. Memory: loops/motion-audit-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
