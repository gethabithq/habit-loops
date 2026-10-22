---
name: supabase-server
title: Supabase Server skill
repo: supabase/server
license: MIT
url: https://gethabit.dev/skills/supabase/supabase-server
---

# Supabase Server skill

The Supabase Server skill (supabase-server) guides an agent writing server-side code with @supabase/server: Edge Functions and backend handlers that pick an auth mode, create Supabase clients and verify inbound auth, and migrate legacy patterns. For backend developers on Supabase.

- Install the skill: `npx skills add supabase/server --skill supabase-server`
- Source: https://github.com/supabase/server/tree/HEAD/skills/supabase-server
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You write a Supabase Edge Function; You pick an auth mode for a handler; You migrate legacy Deno.serve code.
Skip it when: You write only client-side Supabase code; You do first-time project setup.

# Make it a habit: Edge Function auth stays correct.

When a pull request touches files under supabase/functions, the agent checks each one against the @supabase/server rules: a stated auth mode, verify_jwt matched to it, new API keys not legacy ones, and signature checks behind auth none. The build must pass and findings go into a log.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** edge function changes (event; GitHub Actions or Claude Code routine; `pull_request paths: supabase/functions/**`)
- **Verification:** build and auth-mode checks. Hard checks: build passes; every handler sets an auth mode of user, publishable, secret or none; no legacy 'always' or 'public' mode or SUPABASE_ANON_KEY / SUPABASE_SERVICE_ROLE_KEY remains; functions using publishable, secret or none set verify_jwt false in config.toml. On fail: notify, max 1 retries.
- **Memory:** auth review log at `loops/supabase-server-auth-review-loop/log.md`. Read first: auth findings from earlier pull requests.

## Steps

1. **List changes.** Collect the changed files under supabase/functions and any config.toml edits.
2. **Check auth mode.** Confirm each handler states an auth mode and does not fall back to a neighbour's value.
3. **Check verify_jwt.** Confirm config.toml sets verify_jwt false for publishable, secret or none handlers.
4. **Check keys.** Flag legacy keys and legacy mode values and the renamed authType field.
5. **Check public endpoints.** Confirm auth none handlers verify a webhook signature or are truly public.
6. **Build and log.** Run the build, comment the findings and add them to the log.

Stop rule: Stops after one pull request per run and at most 1 build retry.

## Permissions

- Writes: loops/supabase-server-auth-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/supabase-server-auth-review-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: edge function changes. Verification: build and auth-mode checks. Memory: loops/supabase-server-auth-review-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
