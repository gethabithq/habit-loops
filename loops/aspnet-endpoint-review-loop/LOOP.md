---
name: dotnet-webapi
title: ASP.NET Core Web API skill
repo: dotnet/skills
license: MIT
url: https://gethabit.dev/skills/dotnet/dotnet-webapi
---

# ASP.NET Core Web API skill

Dotnet webapi guides creating and changing ASP.NET Core Web API endpoints with correct HTTP semantics, sealed record DTOs, OpenAPI metadata, RFC 7807 error handling and .http test files. For .NET developers building HTTP APIs.

- Install the skill: `npx skills add dotnet/skills --skill dotnet-webapi`
- Source: https://github.com/dotnet/skills/tree/HEAD/plugins/dotnet-aspnetcore/skills/dotnet-webapi
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You add a Web API endpoint; You wire up OpenAPI docs; You set up global error handling.
Skip it when: You work on Blazor or gRPC; You tune EF Core queries.

# Make it a habit: New API endpoints follow HTTP conventions.

On pull requests that add or change ASP.NET Core Web API endpoints, your agent checks HTTP status codes, CancellationToken, sealed record DTOs, OpenAPI metadata and RFC 7807 errors, then builds. A .http test file and the build must pass.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** API endpoint change (event; GitHub Actions or Claude Code routine; `pull_request paths: **/*Controller.cs, Program.cs, **/Endpoints/**`)
- **Verification:** build + convention checks. Hard checks: dotnet build passes with zero errors and zero warnings; every POST create returns 201 with a Location header; every endpoint signature takes a CancellationToken; no domain entity is exposed directly in a request or response body; a .http file has a request for every new endpoint. On fail: notify, max 0 retries.
- **Memory:** endpoint review log at `loops/aspnet-endpoint-review-loop/log.md`. Read first: the project's API style, controllers or minimal APIs, and open findings.

## Steps

1. **Detect the style.** Scan for ControllerBase or app.MapGet to see whether the project uses controllers or minimal APIs, and do not mix them.
2. **Check DTOs.** Confirm request and response types are sealed records with XML summaries and DateTimeOffset for dates.
3. **Check HTTP semantics.** Confirm status codes, Location headers on create, and a CancellationToken forwarded to async calls.
4. **Check OpenAPI.** Confirm endpoints carry summary and description metadata and enums serialize as strings.
5. **Check errors.** Confirm a global exception handler returns RFC 7807 Problem Details and lives in the Middleware folder.
6. **Build and test.** Run dotnet build, load the OpenAPI document and run the .http requests.

Stop rule: Stops after the changed endpoints of one pull request.

## Permissions

- Writes: loops/aspnet-endpoint-review-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/aspnet-endpoint-review-loop/log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: API endpoint change. Verification: build + convention checks. Memory: loops/aspnet-endpoint-review-loop/log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
