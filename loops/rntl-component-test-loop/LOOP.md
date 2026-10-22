---
name: react-native-testing
title: React Native Testing skill
repo: callstack/react-native-testing-library
license: MIT
url: https://gethabit.dev/skills/callstack/react-native-testing
---

# React Native Testing skill

The react native testing skill writes and fixes component tests with React Native Testing Library v13 and v14: render and screen, query priority, Jest matchers, userEvent, fireEvent, waitFor and async patterns. For React Native developers writing tests.

- Install the skill: `npx skills add callstack/react-native-testing-library --skill react-native-testing`
- Source: https://github.com/callstack/react-native-testing-library/tree/HEAD/skills/react-native-testing
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You write React Native component tests; You fix failing RNTL tests; You migrate tests to RNTL v14.
Skip it when: You test React web components; You run end-to-end device tests.

# Make it a habit: Keep React Native components covered.

When a React Native component changes, your agent checks the installed RNTL version, loads the matching v13 or v14 reference, writes tests with screen queries in priority order, userEvent and findBy, applies the rules and anti-patterns, and runs the tests.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** a component changes (event; Claude Code routine; `pull request changes React Native component files`)
- **Verification:** tests pass, rules kept. Hard checks: tests pass; no side-effects inside waitFor; no manual act() or cleanup() calls; queryBy used only for not-on-screen checks. On fail: retry, max 2 retries.
- **Memory:** test log at `loops/rntl-component-test-loop/tests.md`. Read first: RNTL version and custom render wrappers.

## Steps

1. **Detect the version.** Your agent reads @testing-library/react-native from package.json.
2. **Load the reference.** It loads references/api-reference-v14.md or references/api-reference-v13.md.
3. **Write queries.** It uses screen with getByRole first and getByTestId last.
4. **Simulate use.** It uses userEvent, with fireEvent only for unsupported events and fake timers for presses.
5. **Check anti-patterns.** It compares the tests to references/anti-patterns.md.
6. **Run tests.** It runs the tests and fixes failures.

Stop rule: Stops after the changed components and 2 fix rounds per run.

## Permissions

- Writes: **/__tests__/**, **/*.test.tsx, loops/rntl-component-test-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/rntl-component-test-loop/tests.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: a component changes. Verification: tests pass, rules kept. Memory: loops/rntl-component-test-loop/tests.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
