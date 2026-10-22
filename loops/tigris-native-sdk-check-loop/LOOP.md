---
name: tigris-sdk-guide
title: Tigris SDK Guide skill
repo: tigrisdata/skills
license: MIT
url: https://gethabit.dev/skills/tigrisdata/tigris-sdk-guide
---

# Tigris SDK Guide skill

The tigris sdk guide skill tells the agent which SDK to use with Tigris per language: native SDKs for TypeScript and Go, a boto3 extension for Python, AWS SDKs only for Ruby and PHP, and the tigris CLI instead of aws s3. For developers.

- Install the skill: `npx skills add tigrisdata/skills --skill tigris-sdk-guide`
- Source: https://github.com/tigrisdata/skills/tree/HEAD/skills/tigris-sdk-guide
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: you pick a storage SDK; you replace aws s3 commands; you configure Ruby or PHP for Tigris.
Skip it when: you need full SDK reference; you do not use Tigris.

# Make it a habit: Code uses native Tigris SDKs.

When a pull request adds storage dependencies or scripts, the agent checks them against the Tigris SDK decision table: native SDK for TypeScript and Go, tigris-boto3-ext for Python, the tigris CLI instead of aws s3, and region auto. It logs each mismatch.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** PR changes storage dependencies (event; GitHub Actions or Claude Code routine; `pull request changing package manifests or storage scripts`)
- **Verification:** decision table check. Hard checks: no @aws-sdk/client-s3 in JS or TS when @tigrisdata/storage fits; no aws s3 commands in scripts; AWS SDK configs for Ruby and PHP use https://t3.storage.dev, region auto and path style true. On fail: notify, max 0 retries.
- **Memory:** SDK mismatch log at `loops/tigris-native-sdk-check-loop/log.md`. Read first: languages in the repo and mismatches found before.

## Steps

1. **Read the log.** Open the log for the repo's languages and past mismatches.
2. **Map languages.** Match each language in the diff to its row in the decision table.
3. **Check JS and Go.** Confirm @tigrisdata/storage or github.com/tigrisdata/storage-go instead of the AWS SDKs.
4. **Check Python.** Confirm boto3 comes with tigris-boto3-ext when Tigris features are needed.
5. **Check CLI usage.** Flag aws s3 commands that should use tigris or t3.
6. **Check S3 settings.** For Ruby and PHP, confirm the Tigris endpoint, region auto and path style.
7. **Log mismatches.** Write each mismatch with file and suggested package.

Stop rule: One pull request per run, one pass over changed files.

## Permissions

- Writes: loops/tigris-native-sdk-check-loop/
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/tigris-native-sdk-check-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: PR changes storage dependencies. Verification: decision table check. Memory: loops/tigris-native-sdk-check-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
