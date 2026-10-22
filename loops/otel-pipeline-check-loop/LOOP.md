---
name: opentelemetry
title: OpenTelemetry skill
repo: grafana/skills
license: Apache-2.0
url: https://gethabit.dev/skills/grafana/opentelemetry
---

# OpenTelemetry skill

The opentelemetry skill from Grafana shows how to instrument apps with OpenTelemetry and send metrics, logs and traces to Grafana Cloud or self-hosted backends: SDK auto-instrumentation, OTLP auth, Alloy, the Kubernetes Operator and sampling. For teams adding observability.

- Install the skill: `npx skills add grafana/skills --skill opentelemetry`
- Source: https://github.com/grafana/skills/tree/HEAD/skills/grafana-core/opentelemetry
- Licence: Apache-2.0 (Habit links to this skill and does not host or change it)

Use it when: You instrument a service with OTel; You point OTLP at Grafana Cloud; Spans are not showing in Explore.
Skip it when: You do not use Grafana backends; You need app-level logging only.

# Make it a habit: Know telemetry still reaches Grafana.

Each day your agent smoke-tests the Grafana Cloud OTLP endpoint with an empty POST expecting 400, checks Alloy forwarded spans on its metrics page, and confirms traces and metrics for each service in Explore. A log keeps results and auth errors.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** daily telemetry check (schedule; Claude Code routine or cron; `0 7 * * *`)
- **Verification:** OTLP and span checks. Hard checks: OTLP smoke test returns 400, not 401 or 404; otelcol_exporter_sent_spans is above zero on Alloy metrics; TraceQL query for service.name returns spans. On fail: notify, max 1 retries.
- **Memory:** telemetry check log at `loops/otel-pipeline-check-loop/runs.md`. Read first: last result per service and past auth errors.

## Steps

1. **Check env vars.** Your agent confirms OTEL_EXPORTER_OTLP_ENDPOINT, PROTOCOL, HEADERS and RESOURCE_ATTRIBUTES are set.
2. **Smoke test auth.** It POSTs an empty body to the traces endpoint and expects 400.
3. **Check Alloy.** It reads Alloy metrics on localhost:12345 for sent spans.
4. **Check Explore.** It runs TraceQL and PromQL queries for each service.name.
5. **Troubleshoot.** On 401, 404 or missing spans it follows the troubleshooting list.
6. **Log.** It records results per service.

Stop rule: Stops after 10 services per run.

## Permissions

- Writes: loops/otel-pipeline-check-loop/**
- Network: grafana.net, localhost
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/otel-pipeline-check-loop/runs.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: daily telemetry check. Verification: OTLP and span checks. Memory: loops/otel-pipeline-check-loop/runs.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
