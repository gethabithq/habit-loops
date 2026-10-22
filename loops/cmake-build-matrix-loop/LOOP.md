---
name: cmake
title: CMake skill
repo: mohitmishra786/low-level-dev-skills
license: MIT
url: https://gethabit.dev/skills/mohitmishra786/cmake
---

# CMake skill

Cmake is a skill for C and C++ developers who write modern target-first CMakeLists.txt files: out-of-source builds, generators, dependencies with find_package and FetchContent, sanitizers, cross-compilation and presets.

- Install the skill: `npx skills add mohitmishra786/low-level-dev-skills --skill cmake`
- Source: https://github.com/mohitmishra786/low-level-dev-skills/tree/HEAD/skills/build-systems/cmake
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You write a CMakeLists.txt; CMake cannot find a package; You enable sanitizers.
Skip it when: You use another build system; You need Ninja internals.

# Make it a habit: Green C++ builds in every config.

On each pull request, your agent configures out-of-source builds with CMake presets, builds Debug with AddressSanitizer and Release, and reviews CMakeLists.txt changes for target-first style. A log keeps configure errors and fixes.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** pull request opened (event; GitHub Actions; `pull_request.opened`)
- **Verification:** presets build, tests pass. Hard checks: cmake --preset release configures; cmake --build --preset release succeeds; the ENABLE_ASAN debug build succeeds; no include_directories() or link_libraries() in changed files. On fail: notify, max 1 retries.
- **Memory:** configure error log at `loops/cmake-build-matrix-loop/run-log.md`. Read first: recent configure errors and their fixes.

## Steps

1. **Review CMake changes.** Check changed CMakeLists.txt files use target_* commands with PUBLIC, PRIVATE or INTERFACE.
2. **Configure release.** Run cmake --preset release.
3. **Build release.** Run cmake --build --preset release.
4. **Build with ASan.** Configure with -DENABLE_ASAN=ON into build-asan and build it.
5. **Map errors.** Match failures to the skill's common errors table and log the fix.

Stop rule: Stops after one pull request per run, with one retry.

## Permissions

- Writes: build/**, loops/cmake-build-matrix-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/cmake-build-matrix-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: pull request opened. Verification: presets build, tests pass. Memory: loops/cmake-build-matrix-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
