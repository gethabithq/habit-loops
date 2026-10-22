---
name: react-code-review
title: React Code Review skill
repo: giuseppe-trisciuoglio/developer-kit
license: MIT
url: https://gethabit.dev/skills/giuseppe-trisciuoglio/react-code-review
---

# React Code Review skill

React code review checks React components, hooks, React 19 patterns, state management, performance, accessibility and TypeScript props, producing severity-ranked findings with code examples. For developers reviewing React changes before merge.

- Install the skill: `npx skills add giuseppe-trisciuoglio/developer-kit --skill react-code-review`
- Source: https://github.com/giuseppe-trisciuoglio/developer-kit/tree/HEAD/plugins/developer-kit-typescript/skills/react-code-review
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You review React components; You check hook dependency arrays; You validate component architecture.
Skip it when: You do not use React; You want a backend review.

# Make it a habit: React changes reviewed before merge.

On pull requests that touch React components, your agent reviews component architecture, hook usage, state management, accessibility, performance and TypeScript props, and produces findings by severity with code examples. A log keeps open warnings.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** React files change (event; GitHub Actions or Claude Code routine; `pull_request paths: **/*.tsx, **/*.jsx`)
- **Verification:** review report structure. Hard checks: every useEffect, useMemo and useCallback has a correct dependency array; no component prop is typed as any; the report groups findings by severity with code examples; the count of critical issues is zero. On fail: notify, max 0 retries.
- **Memory:** component review log at `loops/react-component-review-loop/log.md`. Read first: open warnings and the project's React version.

## Steps

1. **Identify scope.** Find the changed components and hooks with glob and grep.
2. **Check architecture.** Flag components over 200 lines, more than 7 props or mixed concerns.
3. **Check hooks and state.** Check dependency arrays, cleanup functions and server state using TanStack Query instead of useEffect plus useState.
4. **Check accessibility.** Check semantic HTML, ARIA, keyboard access and labelled inputs.
5. **Check performance and types.** Flag needless re-renders, missing memo where measured, and any typed props.
6. **Write the report.** Group findings as critical, warning and suggestion with code examples and positives.

Stop rule: Stops after the changed components of one pull request.

## Permissions

- Writes: loops/react-component-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/react-component-review-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: React files change. Verification: review report structure. Memory: loops/react-component-review-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
