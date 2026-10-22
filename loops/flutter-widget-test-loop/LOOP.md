---
name: flutter-add-widget-test
title: Flutter Add Widget Test skill
repo: flutter/agent-plugins
license: BSD-3-Clause
url: https://gethabit.dev/skills/flutter/flutter-add-widget-test
---

# Flutter Add Widget Test skill

The flutter add widget test skill writes component tests with WidgetTester, finders and matchers to check rendering, taps, scrolling and text input. For Flutter developers who want each widget covered.

- Install the skill: `npx skills add flutter/agent-plugins --skill flutter-add-widget-test`
- Source: https://github.com/flutter/agent-plugins/tree/HEAD/skills/flutter-add-widget-test
- Licence: BSD-3-Clause (Habit links to this skill and does not host or change it)

Use it when: You add or change a Flutter widget; You test taps or text input; You test a list or animation.
Skip it when: You need a full app flow test; The app is not Flutter.

# Make it a habit: Every new widget gets a test.

When a pull request adds or changes a widget, your agent writes a widget test with WidgetTester: build, find, check, interact, pump and check again. It runs flutter test until the test passes. A board lists widgets still without tests.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR changes a widget (event; GitHub Actions or Claude Code routine; `pull_request paths: lib/**`)
- **Verification:** flutter test passes. Hard checks: flutter test passes for the new test file; test file is in test/ and ends with _test.dart; flutter_test is in dev_dependencies. On fail: retry, max 2 retries.
- **Memory:** untested widgets board at `loops/flutter-widget-test-loop/board.md`. Read first: widgets still without a test.

## Steps

1. **Check setup.** Make sure flutter_test is a dev dependency and tests live in test/.
2. **Define the test.** Write testWidgets and build the widget with tester.pumpWidget.
3. **Check first render.** Use finders and expect to verify the initial state.
4. **Interact.** Tap, drag, enterText or scrollUntilVisible as the widget needs.
5. **Rebuild and check.** Call pump or pumpAndSettle and verify the new state.
6. **Run until green.** Run flutter test on the file and fix failing matchers.

Stop rule: Stops after one widget per run and at most two fix rounds.

## Permissions

- Writes: test/**, pubspec.yaml, loops/flutter-widget-test-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/flutter-widget-test-loop/board.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR changes a widget. Verification: flutter test passes. Memory: loops/flutter-widget-test-loop/board.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
