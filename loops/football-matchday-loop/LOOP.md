---
name: football-data
title: Football Data skill
repo: machina-sports/sports-skills
license: MIT
url: https://gethabit.dev/skills/machina-sports/football-data
---

# Football Data skill

The football data skill gives agents and fans football (soccer) standings, schedules, match stats, xG, transfers, player profiles, head-to-head, Elo strength and forecasts across major leagues, with no API keys.

- Install the skill: `npx skills add machina-sports/sports-skills --skill football-data`
- Source: https://github.com/machina-sports/sports-skills/tree/HEAD/skills/football-data
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You want a league table; You need a match report with xG; You preview an upcoming match.
Skip it when: You need live scores; You ask about American football.

# Make it a habit: Weekly match reports for your teams.

After each matchday your agent resolves your teams with search_team, finds their recent matches, pulls summary, stats and timeline, adds xG for top-5 leagues and previews the next game with head-to-head and strength. A log keeps reported events.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** Monday after matchday (schedule; Claude Code routine or cron; `0 8 * * 1`)
- **Verification:** IDs resolved, scores reconciled. Hard checks: season_id comes from get_current_season; team IDs come from search_team; timeline goal + penalty_goal + own_goal count matches the score; count of reported matches is above zero. On fail: retry, max 1 retries.
- **Memory:** reported events log at `loops/football-matchday-loop/run-log.md`. Read first: team IDs and event IDs already reported.

## Steps

1. **Resolve IDs.** Get season IDs with get_current_season and team IDs with search_team.
2. **Find matches.** Use get_team_schedule to find closed events since the last run.
3. **Build reports.** Call get_event_summary, get_event_statistics and get_event_timeline, plus get_event_xg for top-5 leagues.
4. **Preview next.** Add get_head_to_head, get_team_strength and get_match_forecast where covered.
5. **Write.** Write the report and skip any piece a source does not cover.

Stop rule: Stops after 5 teams per run.

## Permissions

- Writes: loops/football-matchday-loop/**
- Network: football-data.co.uk
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/football-matchday-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: Monday after matchday. Verification: IDs resolved, scores reconciled. Memory: loops/football-matchday-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
