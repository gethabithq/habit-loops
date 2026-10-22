# habit-loops

Ready habits for coding agents, from [Habit](https://gethabit.dev). A habit runs a skill by itself: a trigger starts it, a check proves the work, a memory keeps notes for the next run.

516 habits. Each folder holds one `LOOP.md`. Your agent reads it and sets the habit up with you:

```
Read https://gethabit.dev/LOOP.md and set up Habit as it describes.
```

Or point your agent at one file, for example `loops/plan-grill-loop/LOOP.md`.

The skills inside each habit belong to their authors and are installed from their original repos. Habit links them and never copies or changes them. Every habit was checked against its skill by two independent reviews before it was published.

| Habit | Outcome | Starts | On Habit |
|---|---|---|---|
| [Agent build check loop](loops/agent-build-check-loop/LOOP.md) | LangChain agents built the current way. | PR touches agent code | [page](https://gethabit.dev/skills/langchain-ai/langchain-fundamentals) |
| [Agent CLI ergonomics loop](loops/agent-cli-ergonomics-loop/LOOP.md) | Agent-facing CLIs stay AXI-compliant. | CLI code changes | [page](https://gethabit.dev/skills/kunchenguid/axi) |
| [Agent deploy loop](loops/agent-deploy-loop/LOOP.md) | Agents deployed only after your approval. | eval scores ready | [page](https://gethabit.dev/skills/google/google-agents-cli-deploy) |
| [Agent health audit loop](loops/agent-health-audit-loop/LOOP.md) | Weekly agent setup health report. | weekly health audit | [page](https://gethabit.dev/skills/tw93/health) |
| [Agent orient brief loop](loops/agent-orient-brief-loop/LOOP.md) | Agents know code owners before editing. | new coding task starts | [page](https://gethabit.dev/skills/trkbt10/indexion-agent-orient) |
| [Agent Reach topic watch loop](loops/agent-reach-topic-watch-loop/LOOP.md) | Fresh cross-platform research, read-only. | daily topic scan | [page](https://gethabit.dev/skills/panniantong/skill) |
| [Agent task handoff loop](loops/agent-task-handoff-loop/LOOP.md) | Tasks handed between agents through logstream. | you delegate a task | [page](https://gethabit.dev/skills/mempalace/mempalace-task) |
| [Agent workspace backup loop](loops/agent-workspace-backup-loop/LOOP.md) | Agent files backed up, encrypted, restorable. | weekly agent backup | [page](https://gethabit.dev/skills/theagentservice/openclaw-backup) |
| [AGENTS.md refresh loop](loops/agents-md-refresh-loop/LOOP.md) | Agent docs match the codebase. | weekly docs refresh | [page](https://gethabit.dev/skills/tursodatabase/index-knowledge) |
| [AGENTS.md upkeep loop](loops/agents-md-upkeep-loop/LOOP.md) | Keep agent instructions short, accurate. | monthly instructions review | [page](https://gethabit.dev/skills/getsentry/agents-md) |
| [Agents SDK review loop](loops/agents-sdk-review-loop/LOOP.md) | Cloudflare agents reviewed on every change. | PR touches agent code | [page](https://gethabit.dev/skills/cloudflare/agents-sdk) |
| [AI news digest loop](loops/ai-news-digest-loop/LOOP.md) | A daily digest of AI news. | daily AI digest | [page](https://gethabit.dev/skills/kkkkhazix/aihot) |
| [AI slop cleanup loop](loops/ai-slop-cleanup-loop/LOOP.md) | Bloated AI code trimmed, behavior kept. | after AI code lands | [page](https://gethabit.dev/skills/yeachan-heo/ai-slop-cleaner) |
| [AI visibility loop](loops/ai-visibility-loop/LOOP.md) | Know where AI answers cite you. | monthly visibility check | [page](https://gethabit.dev/skills/coreyhaines31/ai-seo) |
| [Allium converge loop](loops/allium-converge-loop/LOOP.md) | Spec, tests and code all agree. | you give a goal | [page](https://gethabit.dev/skills/juxt/allium) |
| [Allium distill loop](loops/allium-distill-loop/LOOP.md) | Existing code gets a spec. | module needs a spec | [page](https://gethabit.dev/skills/juxt/distill) |
| [Allium propagate loop](loops/allium-propagate-loop/LOOP.md) | Spec changes regenerate the tests. | allium spec changed | [page](https://gethabit.dev/skills/juxt/propagate) |
| [Allium spec drift loop](loops/allium-spec-drift-loop/LOOP.md) | Spec and code stay aligned. | weekly drift check | [page](https://gethabit.dev/skills/juxt/weed) |
| [Allium tend loop](loops/allium-tend-loop/LOOP.md) | Spec changes stay valid. | spec change requested | [page](https://gethabit.dev/skills/juxt/tend) |
| [Amazon listing audit loop](loops/amazon-listing-audit-loop/LOOP.md) | Listings keep their keyword coverage. | monthly listing audit | [page](https://gethabit.dev/skills/nexscope-ai/amazon-listing-optimization) |
| [Amazon product watch loop](loops/amazon-product-watch-loop/LOOP.md) | Fresh scores for watched products. | every Monday | [page](https://gethabit.dev/skills/nexscope-ai/amazon-product-research) |
| [Animation opportunities loop](loops/animation-opportunities-loop/LOOP.md) | Only motion that earns its place. | weekly UI sweep | [page](https://gethabit.dev/skills/emilkowalski/find-animation-opportunities) |
| [antd API check loop](loops/antd-api-check-loop/LOOP.md) | antd code uses real, current APIs. | antd code changes | [page](https://gethabit.dev/skills/ant-design/ant-design) |
| [Ant Design lint loop](loops/antd-lint-loop/LOOP.md) | Keep antd usage current and clean. | antd code changes | [page](https://gethabit.dev/skills/ant-design/antd) |
| [Antigravity task queue loop](loops/antigravity-task-queue-loop/LOOP.md) | Delegate to agy, review, then land. | you queue tasks for agy | [page](https://gethabit.dev/skills/amelnagdy/agy-delegate) |
| [Antislop audit loop](loops/antislop-audit-loop/LOOP.md) | Strip generic AI look from UI. | UI work finished | [page](https://gethabit.dev/skills/miqdadbadjuber/antislop) |
| [Antislop mobile layout loop](loops/antislop-mobile-layout-loop/LOOP.md) | Layouts that reflow at every width. | layout code changes | [page](https://gethabit.dev/skills/miqdadbadjuber/antislop-layoutmobile) |
| [AnySearch watch loop](loops/anysearch-watch-loop/LOOP.md) | Fresh facts on your topics. | daily topic search | [page](https://gethabit.dev/skills/anysearch-ai/anysearch) |
| [APM slow trace loop](loops/apm-slow-trace-loop/LOOP.md) | Slow and failing services flagged daily. | daily trace check | [page](https://gethabit.dev/skills/datadog-labs/dd-apm) |
| [App review health loop](loops/app-review-health-loop/LOOP.md) | Submission blockers found and routed. | validation fails or stalls | [page](https://gethabit.dev/skills/rorkai/asc-submission-health) |
| [App smoke flow loop](loops/app-smoke-flow-loop/LOOP.md) | Every build passes a real tap-through. | new app build ready | [page](https://gethabit.dev/skills/callstack/agent-device) |
| [Apply upgrade notes loop](loops/apply-upgrade-notes-loop/LOOP.md) | Installed pipeline artifacts stay current. | after skills upgrade | [page](https://gethabit.dev/skills/open-mercato/om-apply-upgrade-notes) |
| [Appwrite code review loop](loops/appwrite-code-review-loop/LOOP.md) | Appwrite code follows current SDK patterns. | Appwrite code changed | [page](https://gethabit.dev/skills/appwrite/appwrite-typescript) |
| [Appwrite schema sync loop](loops/appwrite-schema-sync-loop/LOOP.md) | Schema, config and types stay synced. | config file changes | [page](https://gethabit.dev/skills/appwrite/appwrite-cli) |
| [Architecture diagram loop](loops/archify-diagram-loop/LOOP.md) | Diagrams that match the code. | push to main | [page](https://gethabit.dev/skills/tt-a1i/archify) |
| [Architect decision spec loop](loops/architect-decision-spec-loop/LOOP.md) | Turn open decisions into build specs. | decision owed or Assumed | [page](https://gethabit.dev/skills/jsmastery-pro/architect) |
| [Architecture deepening loop](loops/architecture-deepening-loop/LOOP.md) | Find shallow modules, deepen one. | weekly architecture review | [page](https://gethabit.dev/skills/mattpocock/improve-codebase-architecture) |
| [Architecture diagram loop](loops/architecture-diagram-loop/LOOP.md) | Keep diagrams true to the code. | merge to main | [page](https://gethabit.dev/skills/tt-a1i/archify) |
| [Architecture drift audit loop](loops/architecture-drift-audit-loop/LOOP.md) | Code keeps to your ADRs. | PR opened or updated | [page](https://gethabit.dev/skills/stark-ai-de/architecture-compass) |
| [Arize error trace digest loop](loops/arize-error-trace-digest-loop/LOOP.md) | A daily digest of failing traces. | daily error digest | [page](https://gethabit.dev/skills/arize-ai/arize-trace) |
| [Arize eval check loop](loops/arize-eval-check-loop/LOOP.md) | Score new spans every week. | every Monday morning | [page](https://gethabit.dev/skills/arize-ai/arize-evaluator) |
| [Arize eval dataset loop](loops/arize-eval-dataset-loop/LOOP.md) | A growing, verified evaluation dataset. | new test cases added | [page](https://gethabit.dev/skills/arize-ai/arize-dataset) |
| [Art direction sign-off loop](loops/art-direction-signoff-loop/LOOP.md) | An agreed look before volume generation. | new brief arrives | [page](https://gethabit.dev/skills/layerai/layer-art-direction) |
| [App Store release loop](loops/asc-release-loop/LOOP.md) | Releases reach review safely. | release approved | [page](https://gethabit.dev/skills/rorkai/asc-release-flow) |
| [ASP.NET endpoint review loop](loops/aspnet-endpoint-review-loop/LOOP.md) | New API endpoints follow HTTP conventions. | API endpoint change | [page](https://gethabit.dev/skills/dotnet/dotnet-webapi) |
| [Astro hydration review loop](loops/astro-hydration-review-loop/LOOP.md) | Astro pages ship only needed JavaScript. | Astro pull request | [page](https://gethabit.dev/skills/delineas/astro-framework) |
| [Dependency audit loop](loops/audit-dependencies-loop/LOOP.md) | Vulnerable dependencies fixed the simplest way. | audit check fails | [page](https://gethabit.dev/skills/payloadcms/audit-dependencies) |
| [Page speed audit loop](loops/audit-speed-loop/LOOP.md) | Core Web Vitals checked every week. | weekly speed audit | [page](https://gethabit.dev/skills/calm-north/audit-speed) |
| [Auth0 tenant audit loop](loops/auth0-tenant-audit-loop/LOOP.md) | Tenant security issues found monthly. | monthly tenant audit | [page](https://gethabit.dev/skills/auth0/auth0) |
| [Auto create PR loop](loops/auto-create-pr-loop-habit/LOOP.md) | Task brief shipped as a PR | you give a task brief | [page](https://gethabit.dev/skills/open-mercato/om-auto-create-pr) |
| [Automation recommender loop](loops/automation-recommender-loop/LOOP.md) | Fresh automation ideas every month. | first day each month | [page](https://gethabit.dev/skills/anthropics/claude-automation-recommender) |
| [Baidu news digest loop](loops/baidu-news-digest-loop/LOOP.md) | Weekly Chinese news digest per topic. | weekly topic digest | [page](https://gethabit.dev/skills/countbot-ai/baidu-search) |
| [Bailian agents.yaml loop](loops/bailian-agents-yaml-loop/LOOP.md) | Agent infra changes stay reviewed. | agents.yaml changed | [page](https://gethabit.dev/skills/modelstudioai/bailian-managed-agent) |
| [Bailian media batch loop](loops/bailian-media-batch-loop/LOOP.md) | Media requests become saved files. | new media request list | [page](https://gethabit.dev/skills/modelstudioai/bailian-gen) |
| [Bailian usage watch loop](loops/bailian-usage-watch-loop/LOOP.md) | Know your Bailian usage weekly. | every Monday morning | [page](https://gethabit.dev/skills/modelstudioai/bailian-cli) |
| [Base44 error sweep loop](loops/base44-error-sweep-loop/LOOP.md) | Catch Base44 failures each morning. | every morning | [page](https://gethabit.dev/skills/base44/base44-troubleshooter) |
| [Baseline UI review loop](loops/baseline-ui-review-loop/LOOP.md) | UI slop gets caught on merge. | PR touches UI files | [page](https://gethabit.dev/skills/ibelick/baseline-ui) |
| [Beat sync edit loop](loops/beat-sync-edit-loop/LOOP.md) | Every cut lands on beat. | track and footage ready | [page](https://gethabit.dev/skills/iart-ai/beat-sync-editing) |
| [Bitbucket PR status loop](loops/bitbucket-pr-status-loop/LOOP.md) | Failing Bitbucket PRs flagged daily. | workday PR check | [page](https://gethabit.dev/skills/avivsinai/bkt) |
| [Blender model check loop](loops/blender-model-check-loop/LOOP.md) | Clean meshes built step by step. | new object to model | [page](https://gethabit.dev/skills/roble3/blender-modeling) |
| [Book breakdown loop](loops/book-breakdown-loop/LOOP.md) | Reference novels broken down in stages. | novel text added | [page](https://gethabit.dev/skills/zenstory-ai/story-long-analyze) |
| [Book fold-in loop](loops/book-fold-in-loop/LOOP.md) | Keep book skills up to date. | new document added | [page](https://gethabit.dev/skills/virgiliojr94/book-to-skill) |
| [Book study review loop](loops/book-study-review-loop/LOOP.md) | Book concepts held in long-term memory. | you open the book | [page](https://gethabit.dev/skills/sanyuan0704/book-study) |
| [Book to skills loop](loops/book-to-skills-loop/LOOP.md) | One book distilled into usable skills. | next book on board | [page](https://gethabit.dev/skills/kangarooking/cangjie-skill) |
| [Botpress ADK health loop](loops/botpress-adk-health-loop/LOOP.md) | ADK bot checked before every session. | ADK session starts | [page](https://gethabit.dev/skills/botpress/adk) |
| [Brag launch video loop](loops/brag-slim-launch-video-loop/LOOP.md) | A launch video per release. | new feature or release | [page](https://gethabit.dev/skills/latent-spaces/brag-slim) |
| [Branch bug hunt loop](loops/branch-bug-hunt-loop/LOOP.md) | Find bugs before branches merge. | pull request opened | [page](https://gethabit.dev/skills/getsentry/find-bugs) |
| [Brave news watch loop](loops/brave-news-watch-loop/LOOP.md) | Fresh results on your topics, daily. | daily topic search | [page](https://gethabit.dev/skills/brave/web-search) |
| [Breach self-audit loop](loops/breach-self-audit-loop/LOOP.md) | Know when your accounts leak. | monthly breach check | [page](https://gethabit.dev/skills/useosint/what-leaked-about-you) |
| [Brief to tasks loop](loops/brief-to-tasks-loop/LOOP.md) | Turn design briefs into buildable tasks. | a brief is written | [page](https://gethabit.dev/skills/julianoczkowski/brief-to-tasks) |
| [Bright Data search loop](loops/bright-data-search-loop/LOOP.md) | Fresh search results, checked. | weekly query run | [page](https://gethabit.dev/skills/brightdata/search) |
| [Browser QA loop](loops/browser-qa-loop/LOOP.md) | Your web app tested every night. | nightly app check | [page](https://gethabit.dev/skills/vercel-labs/agent-browser) |
| [Business analytics report loop](loops/business-analytics-report-loop/LOOP.md) | Monthly report on weak business areas. | monthly sales report | [page](https://gethabit.dev/skills/ailabs-393/business-analytics-reporter) |
| [Cache Components adoption loop](loops/cache-components-adoption-loop/LOOP.md) | One feature adopted per run. | next feature to adopt | [page](https://gethabit.dev/skills/vercel/next-cache-components-adoption) |
| [Calendar agenda loop](loops/calendar-agenda-loop/LOOP.md) | Start each day with your agenda. | weekday morning agenda | [page](https://gethabit.dev/skills/googleworkspace/gws-calendar) |
| [Capacitor health loop](loops/capacitor-health-loop/LOOP.md) | Capacitor app stays release ready. | weekly app review | [page](https://gethabit.dev/skills/cap-go/capacitor-best-practices) |
| [Carousel writing loop](loops/carousel-writing-loop/LOOP.md) | A ready carousel draft every week. | weekly carousel draft | [page](https://gethabit.dev/skills/blacktwist/carousel-writer-sms) |
| [Cavecrew fix loop](loops/cavecrew-fix-loop/LOOP.md) | Small fixes with lean context. | small fix task | [page](https://gethabit.dev/skills/juliusbrussee/cavecrew) |
| [CCXT market snapshot loop](loops/ccxt-market-snapshot-loop/LOOP.md) | Daily read-only market snapshots. | every morning | [page](https://gethabit.dev/skills/ccxt/ccxt-cli) |
| [Celigo export check loop](loops/celigo-export-check-loop/LOOP.md) | Celigo exports keep returning records. | every Monday morning | [page](https://gethabit.dev/skills/celigo/configuring-exports) |
| [Celigo import check loop](loops/celigo-import-check-loop/LOOP.md) | Celigo imports pass their checklist. | every Monday morning | [page](https://gethabit.dev/skills/celigo/configuring-imports) |
| [Chakra UI review loop](loops/chakra-ui-review-loop/LOOP.md) | Components stay accessible and v3-correct. | component files change | [page](https://gethabit.dev/skills/chakra-ui/chakra-ui-refactor) |
| [Change document loop](loops/change-document-loop/LOOP.md) | Every change gets human-facing prose. | change ready to document | [page](https://gethabit.dev/skills/jsmastery-pro/document) |
| [Chinese novel chapter loop](loops/chinese-novel-chapter-loop/LOOP.md) | Write a novel chapter by chapter. | you start or resume | [page](https://gethabit.dev/skills/penglonghuang/chinese-novelist) |
| [Chinese prose polish loop](loops/chinese-prose-polish-loop/LOOP.md) | Chinese drafts read natural, facts kept. | Chinese draft changed | [page](https://gethabit.dev/skills/op7418/humanizer-zh) |
| [CI bottleneck weekly report](loops/ci-bottleneck-weekly-loop/LOOP.md) | CI long pole named weekly. | weekly CI health | [page](https://gethabit.dev/skills/posthog/diagnosing-ci-and-merge-bottlenecks) |
| [CI flake triage loop](loops/ci-flake-triage-loop/LOOP.md) | Flaky e2e tests reproduced, then fixed. | e2e fails on main | [page](https://gethabit.dev/skills/payloadcms/triage-ci-flake) |
| [CI triage loop](loops/ci-triage-loop/LOOP.md) | Failing CI gets triaged fast. | a CI run fails | [page](https://gethabit.dev/skills/paulrberg/cli-gh) |
| [CLAUDE.md audit loop](loops/claude-md-audit-loop/LOOP.md) | Keep every CLAUDE.md current. | weekly on Monday | [page](https://gethabit.dev/skills/anthropics/claude-md-improver) |
| [ClickHouse metrics report loop](loops/clickhouse-metrics-report-loop/LOOP.md) | Weekly metrics with clear definitions. | weekly metrics report | [page](https://gethabit.dev/skills/cline/data-analyst) |
| [CMake build matrix loop](loops/cmake-build-matrix-loop/LOOP.md) | Green C++ builds in every config. | pull request opened | [page](https://gethabit.dev/skills/mohitmishra786/cmake) |
| [Code index refresh loop](loops/code-index-refresh-loop/LOOP.md) | Keep semantic code search fresh. | code changes land | [page](https://gethabit.dev/skills/cocoindex-io/ccc) |
| [Code polish loop](loops/code-polish-loop/LOOP.md) | Changed code ends up simpler. | PR opened or updated | [page](https://gethabit.dev/skills/paulrberg/code-polish) |
| [Codebase advisor loop](loops/codebase-advisor-loop/LOOP.md) | Fresh improvement plans every week. | weekly code audit | [page](https://gethabit.dev/skills/shadcn/improve) |
| [Codebase control loop](loops/codebase-control-loop/LOOP.md) | A scheduled loop driving your codebase. | you want a loop | [page](https://gethabit.dev/skills/humanlayer/design-control-loop) |
| [CodeGraph health check loop](loops/codegraph-health-check-loop/LOOP.md) | Code analysis tools stay ready. | weekly analysis stack check | [page](https://gethabit.dev/skills/stark-ai-de/codegraph-ast-grep) |
| [CodeRabbit autofix loop](loops/coderabbit-autofix-loop/LOOP.md) | Review threads fixed with approval. | CodeRabbit review posted | [page](https://gethabit.dev/skills/coderabbitai/autofix) |
| [Codex memory review loop](loops/codex-memory-review-loop/LOOP.md) | Codex memory stays true and safe. | monthly memory review | [page](https://gethabit.dev/skills/stark-ai-de/codex-memory-curator) |
| [Color contrast audit loop](loops/color-contrast-audit-loop/LOOP.md) | Every color pair passes contrast. | color tokens changed | [page](https://gethabit.dev/skills/owl-listener/color-system) |
| [Color motion loop](loops/color-motion-loop/LOOP.md) | Gradients without muddy midpoints. | new color brief | [page](https://gethabit.dev/skills/iart-ai/color-motion) |
| [Color system audit loop](loops/color-system-audit-loop/LOOP.md) | Color tokens stay used by role. | PR touches styles | [page](https://gethabit.dev/skills/jakubkrehel/better-colors) |
| [Community PR finish loop](loops/community-pr-finish-loop/LOOP.md) | Blocked community PRs get merged. | /finish-line with PR | [page](https://gethabit.dev/skills/remix-run/finish-line) |
| [Console audit loop](loops/console-audit-loop/LOOP.md) | Console errors caught before users. | nightly local audit | [page](https://gethabit.dev/skills/sentimony/web-debug) |
| [Content brief queue loop](loops/content-brief-queue-loop/LOOP.md) | One editor-ready brief per keyword. | weekly brief batch | [page](https://gethabit.dev/skills/calm-north/brief) |
| [Content calendar loop](loops/content-calendar-loop/LOOP.md) | Next week's posting plan, every Monday. | Monday planning session | [page](https://gethabit.dev/skills/blacktwist/content-calendar-sms) |
| [Content strategy loop](loops/content-strategy-loop/LOOP.md) | A ranked content plan each month. | first of the month | [page](https://gethabit.dev/skills/coreyhaines31/content-strategy) |
| [Content strategy review loop](loops/content-strategy-review-loop/LOOP.md) | A content strategy that stays current. | quarterly strategy review | [page](https://gethabit.dev/skills/blacktwist/content-strategy-sms) |
| [Convex backend review loop](loops/convex-backend-review-loop/LOOP.md) | Every Convex change reviewed and verified. | PR changes convex/ | [page](https://gethabit.dev/skills/convex/convex) |
| [Convex review loop](loops/convex-review-loop/LOOP.md) | Convex changes checked against the rules. | convex code changes | [page](https://gethabit.dev/skills/waynesutton/convex-best-practices) |
| [Convex subscription check loop](loops/convex-subscription-check-loop/LOOP.md) | Live queries stay small and indexed. | PR touches convex code | [page](https://gethabit.dev/skills/waynesutton/convex-realtime) |
| [Page copy loop](loops/copywriting-loop/LOOP.md) | Clear copy without AI tells. | copy brief opened | [page](https://gethabit.dev/skills/coreyhaines31/copywriting) |
| [CrewAI agent review loop](loops/crewai-agent-review-loop/LOOP.md) | Every agent passes the checklist. | agent config changed | [page](https://gethabit.dev/skills/crewaiinc/design-agent) |
| [Crypto price watch loop](loops/crypto-price-watch-loop/LOOP.md) | Live prices streamed, read-only. | daily price snapshot | [page](https://gethabit.dev/skills/ccxt/ccxt-python) |
| [Cursor rules review loop](loops/cursor-rules-review-loop/LOOP.md) | Cursor rules stay current and safe. | monthly Cursor rules review | [page](https://gethabit.dev/skills/stark-ai-de/cursor-memory-curator) |
| [Daily AI news loop](loops/daily-ai-news-loop/LOOP.md) | A fresh AI briefing daily. | every morning | [page](https://gethabit.dev/skills/yyh211/daily-ai-news) |
| [Daily papers digest loop](loops/daily-papers-digest-loop/LOOP.md) | Never miss an important paper. | weekday morning digest | [page](https://gethabit.dev/skills/huggingface/huggingface-papers) |
| [Dark mode check loop](loops/dark-mode-check-loop/LOOP.md) | Dark mode stays readable everywhere. | light theme changed | [page](https://gethabit.dev/skills/owl-listener/dark-mode-design) |
| [Dashboard search first loop](loops/dashboard-search-first-loop/LOOP.md) | No duplicate Coralogix dashboards built. | new dashboard requested | [page](https://gethabit.dev/skills/coralogix/cx-search-dashboard) |
| [Dash discipline loop](loops/dashfix-check-loop/LOOP.md) | Prose uses only the plain hyphen. | prose files changed | [page](https://gethabit.dev/skills/sentimony/dashfix) |
| [Data availability audit loop](loops/data-availability-audit-loop/LOOP.md) | Every dataset has an access route. | before manuscript submission | [page](https://gethabit.dev/skills/yuan1z0825/nature-data) |
| [Decision records check loop](loops/decision-records-check-loop/LOOP.md) | Keep decision records valid and linked. | decision docs change | [page](https://gethabit.dev/skills/skymavis/decision-records) |
| [Deep interview spec loop](loops/deep-interview-spec-loop/LOOP.md) | Vague ideas become clear specs. | you run deep-interview | [page](https://gethabit.dev/skills/yeachan-heo/deep-interview) |
| [Design DNA fidelity loop](loops/design-dna-fidelity-loop/LOOP.md) | Match generated designs to references. | you share references | [page](https://gethabit.dev/skills/zanwei/design-dna) |
| [Design doc check loop](loops/design-doc-check-loop/LOOP.md) | Specs reach reviewers without vague gaps. | design doc pull request | [page](https://gethabit.dev/skills/riekelt/writing-design-docs) |
| [Design-first brainstorm loop](loops/design-first-brainstorm-loop/LOOP.md) | No build before an approved design. | new feature request | [page](https://gethabit.dev/skills/obra/brainstorming) |
| [Design flow phase loop](loops/design-flow-phase-loop/LOOP.md) | Takes features from idea to UI. | you start a feature | [page](https://gethabit.dev/skills/julianoczkowski/design-flow) |
| [Design token guard loop](loops/design-token-guard-loop/LOOP.md) | No hardcoded colors slip in. | PR changes styles | [page](https://gethabit.dev/skills/nextlevelbuilder/design-system) |
| [Devbox test run loop](loops/devbox-test-run-loop/LOOP.md) | Tests run on a disposable devbox. | pull request opened | [page](https://gethabit.dev/skills/namespacelabs/devboxes) |
| [Diagram redraw loop](loops/diagram-design-loop/LOOP.md) | Clean branded diagrams, checked each time. | diagram source changes | [page](https://gethabit.dev/skills/cathrynlavery/diagram-design) |
| [Diff impact review loop](loops/diff-impact-review-loop/LOOP.md) | Every PR gets an impact map. | pull request opened | [page](https://gethabit.dev/skills/egonex-ai/understand-diff) |
| [Discriminated unions review loop](loops/discriminated-unions-review-loop/LOOP.md) | Invalid states removed from the code. | TypeScript changes | [page](https://gethabit.dev/skills/mkosir/typescript-discriminated-unions) |
| [Disk storage report loop](loops/disk-storage-report-loop/LOOP.md) | Know what fills your disk. | monthly disk scan | [page](https://gethabit.dev/skills/kkkkhazix/storage-analyzer) |
| [Docs crawl sync loop](loops/docs-crawl-sync-loop/LOOP.md) | Fresh local copy of docs. | every Monday early | [page](https://gethabit.dev/skills/tavily-ai/tavily-crawl) |
| [Docs review loop](loops/docs-review-loop/LOOP.md) | Every doc reviewed before it ships. | PR changes a document | [page](https://gethabit.dev/skills/riekelt/reviewing-technical-prose) |
| [Domain context loop](loops/domain-context-loop/LOOP.md) | Your agent learns your business. | every session start | [page](https://gethabit.dev/skills/customware-ai/domain-context) |
| [Domain glossary loop](loops/domain-glossary-loop/LOOP.md) | One clear term per concept. | you start design session | [page](https://gethabit.dev/skills/pandoscope/domain-modeling) |
| [.NET test run loop](loops/dotnet-test-run-loop/LOOP.md) | Run the right dotnet test command. | .NET pull request opened | [page](https://gethabit.dev/skills/dotnet/run-tests) |
| [Draft de-slop loop](loops/draft-deslop-loop/LOOP.md) | Drafts sound like you, not AI. | you share a draft | [page](https://gethabit.dev/skills/petergyang/no-ai-slop) |
| [Draw.io diagram loop](loops/drawio-diagram-loop/LOOP.md) | Diagrams stay valid and current. | diagram spec changed | [page](https://gethabit.dev/skills/bahayonghang/drawio) |
| [Draw.io diagram review loop](loops/drawio-diagram-review-loop/LOOP.md) | Diagrams stay valid and readable. | PR changes drawio files | [page](https://gethabit.dev/skills/stark-ai-de/drawio-diagrams) |
| [Drive changes digest loop](loops/drive-changes-digest-loop/LOOP.md) | Know what changed in Drive. | every morning | [page](https://gethabit.dev/skills/googleworkspace/gws-drive) |
| [Duplicate code loop](loops/duplicate-code-loop/LOOP.md) | Copy-pasted code stops growing. | weekly duplication scan | [page](https://gethabit.dev/skills/kucherenko/jscpd) |
| [Durable Objects review loop](loops/durable-objects-review-loop/LOOP.md) | Durable Object code stays safe. | PR touches Durable Objects | [page](https://gethabit.dev/skills/cloudflare/durable-objects) |
| [Dynatrace problem triage loop](loops/dynatrace-problem-triage-loop/LOOP.md) | Active problems triaged every morning. | every morning | [page](https://gethabit.dev/skills/dynatrace/dt-obs-problems) |
| [Dynatrace slow trace loop](loops/dynatrace-slow-trace-loop/LOOP.md) | Slow and failed requests found daily. | every morning | [page](https://gethabit.dev/skills/dynatrace/dt-obs-tracing) |
| [EF Core query review loop](loops/ef-core-query-review-loop/LOOP.md) | Catch slow EF Core queries early. | data access code changes | [page](https://gethabit.dev/skills/dotnet/optimizing-ef-core-queries) |
| [Effect v4 review loop](loops/effect-v4-review-loop/LOOP.md) | Effect code follows v4 defaults. | Effect code changes | [page](https://gethabit.dev/skills/kitlangton/effect) |
| [Electron smoke test loop](loops/electron-smoke-test-loop/LOOP.md) | Desktop app checked after each build. | new Electron build | [page](https://gethabit.dev/skills/vercel-labs/electron) |
| [Email health review loop](loops/email-best-practices-loop/LOOP.md) | Emails stay deliverable and accessible. | weekly email review | [page](https://gethabit.dev/skills/resend/email-best-practices) |
| [Email unsubscribe check loop](loops/email-unsubscribe-check-loop/LOOP.md) | Every marketing mail can unsubscribe. | email code changed | [page](https://gethabit.dev/skills/caffeinelabs/extension-email-marketing) |
| [ES|QL log digest loop](loops/esql-log-digest-loop/LOOP.md) | Daily log patterns and spikes reported. | daily log digest | [page](https://gethabit.dev/skills/elastic/elasticsearch-esql) |
| [Excel merge report loop](loops/excel-merge-report-loop/LOOP.md) | One merged sheet every week. | every Friday afternoon | [page](https://gethabit.dev/skills/texiaoyao/office-automation) |
| [Fallow PR audit loop](loops/fallow-pr-audit-loop/LOOP.md) | Every PR gets a risk verdict. | pull request opened | [page](https://gethabit.dev/skills/fallow-rs/fallow) |
| [FFmpeg platform export loop](loops/ffmpeg-platform-export-loop/LOOP.md) | Each render ready for every platform. | new Remotion render | [page](https://gethabit.dev/skills/digitalsamba/ffmpeg) |
| [File planning loop (Spanish)](loops/file-planning-es-loop/LOOP.md) | Long tasks survive context resets. | multi-step task starts | [page](https://gethabit.dev/skills/othmanadi/planning-with-files-es) |
| [File planning loop](loops/file-planning-loop/LOOP.md) | Long tasks keep plans on disk. | multi-step task starts | [page](https://gethabit.dev/skills/othmanadi/planning-with-files-zh) |
| [Firebase rules audit loop](loops/firebase-rules-audit-loop/LOOP.md) | No rules change ships unaudited. | rules file changed | [page](https://gethabit.dev/skills/firebase/firebase-security-rules-auditor) |
| [Five-axis review loop](loops/five-axis-review-loop/LOOP.md) | Every PR reviewed before merge. | pull request opened | [page](https://gethabit.dev/skills/addyosmani/code-review-and-quality) |
| [Flight fare watch loop](loops/flight-fare-watch-loop/LOOP.md) | See fare changes on your route. | every morning at seven | [page](https://gethabit.dev/skills/skillhq/google-flights) |
| [Flow breadboard loop](loops/flow-breadboard-loop/LOOP.md) | Flows mapped with every edge case. | new job story to map | [page](https://gethabit.dev/skills/jamiemill/layers-interaction-flow) |
| [Flue desktop step loop](loops/flue-desktop-step-loop/LOOP.md) | Desktop app edits, one step. | you request an edit | [page](https://gethabit.dev/skills/sfkislev/flue) |
| [Flutter animation check loop](loops/flutter-animation-check-loop/LOOP.md) | Clean Flutter motion, analyzer approved. | pull request touches animations | [page](https://gethabit.dev/skills/madteacher/flutter-animations) |
| [Flutter layer review loop](loops/flutter-layer-review-loop/LOOP.md) | Flutter features keep clean layer boundaries. | PR changes lib/ | [page](https://gethabit.dev/skills/madteacher/flutter-architecture) |
| [Flutter widget test loop](loops/flutter-widget-test-loop/LOOP.md) | Every new widget gets a test. | PR changes a widget | [page](https://gethabit.dev/skills/flutter/flutter-add-widget-test) |
| [FlyAI trip watch loop](loops/flyai-trip-watch-loop/LOOP.md) | Track flight and hotel options daily. | every morning at seven | [page](https://gethabit.dev/skills/alibaba-flyai/flyai) |
| [Football matchday loop](loops/football-matchday-loop/LOOP.md) | Weekly match reports for your teams. | Monday after matchday | [page](https://gethabit.dev/skills/machina-sports/football-data) |
| [Frontend test review loop](loops/frontend-test-review-loop/LOOP.md) | Tests check behavior, not implementation. | test files changed | [page](https://gethabit.dev/skills/sergiodxa/frontend-testing-best-practices) |
| [Game asset set loop](loops/game-asset-set-loop/LOOP.md) | New assets that match the set. | set needs new assets | [page](https://gethabit.dev/skills/layerai/layer-game-assets) |
| [Game mod build loop](loops/game-mod-build-loop/LOOP.md) | Mods working in the real game. | you name game, idea | [page](https://gethabit.dev/skills/rehan-remade/mod-any-game) |
| [Gemini model freshness loop](loops/gemini-model-freshness-loop/LOOP.md) | No deprecated Gemini models ship. | weekly model scan | [page](https://gethabit.dev/skills/google-gemini/gemini-api-dev) |
| [Terse commit message loop](loops/genshijin-commit-loop/LOOP.md) | Short commit messages that explain why. | changes are staged | [page](https://gethabit.dev/skills/interfacex-co-jp/genshijin-commit) |
| [Memory file compress loop](loops/genshijin-compress-loop/LOOP.md) | Smaller memory files, same facts. | you name a file | [page](https://gethabit.dev/skills/interfacex-co-jp/genshijin-compress) |
| [Terse PR review loop](loops/genshijin-review-loop/LOOP.md) | Short review comments on every PR. | pull request opened | [page](https://gethabit.dev/skills/interfacex-co-jp/genshijin-review) |
| [GitHub issue digest loop](loops/gh-issue-digest-loop/LOOP.md) | Open issues and PRs summarized daily. | daily repo digest | [page](https://gethabit.dev/skills/cli/gh) |
| [GitHub repo digest loop](loops/gh-repo-digest-loop/LOOP.md) | A daily digest of your repo. | daily repo digest | [page](https://gethabit.dev/skills/logicrw/gh-cli) |
| [GHA workflow security loop](loops/gha-workflow-security-loop/LOOP.md) | Exploitable workflow bugs caught before merge. | workflow file changes | [page](https://gethabit.dev/skills/getsentry/gha-security-review) |
| [Go design review loop](loops/go-design-review-loop/LOOP.md) | Go code stays idiomatic and bounded. | weekly design review | [page](https://gethabit.dev/skills/samber/golang-design-patterns) |
| [Go error handling loop](loops/go-error-handling-review-loop/LOOP.md) | No swallowed or double-logged errors. | PR changes Go files | [page](https://gethabit.dev/skills/samber/golang-error-handling) |
| [Go quality gate loop](loops/go-quality-gate-loop/LOOP.md) | Go changes that pass every gate. | PR changes Go files | [page](https://gethabit.dev/skills/jeffallan/golang-pro) |
| [Go style review loop](loops/go-style-review-loop/LOOP.md) | Go code stays clear, not clever. | PR changes Go files | [page](https://gethabit.dev/skills/samber/golang-code-style) |
| [Go test audit loop](loops/go-test-audit-loop/LOOP.md) | Go tests stay fast, isolated, leak-free. | weekly test audit | [page](https://gethabit.dev/skills/samber/golang-testing) |
| [Gradio Space check loop](loops/gradio-space-check-loop/LOOP.md) | Your Gradio endpoints keep answering. | every morning at seven | [page](https://gethabit.dev/skills/huggingface/huggingface-gradio) |
| [GraphQL operations review loop](loops/graphql-operations-review-loop/LOOP.md) | Operations match the schema and lint. | operations change | [page](https://gethabit.dev/skills/apollographql/graphql-operations) |
| [Grill docs loop](loops/grill-docs-loop/LOOP.md) | Plans grilled, decisions documented. | you start a plan | [page](https://gethabit.dev/skills/mattpocock/grill-with-docs) |
| [Groundcover prod triage loop](loops/groundcover-prod-triage-loop/LOOP.md) | Production issues triaged with evidence. | every weekday morning | [page](https://gethabit.dev/skills/paymog/groundcover-cli) |
| [GSAP performance loop](loops/gsap-performance-loop/LOOP.md) | Keep GSAP animations smooth. | PR changes animation code | [page](https://gethabit.dev/skills/greensock/gsap-performance) |
| [GSAP React cleanup loop](loops/gsap-react-cleanup-loop/LOOP.md) | No leaking GSAP animations in React. | PR changes GSAP components | [page](https://gethabit.dev/skills/greensock/gsap-react) |
| [Hallmark design loop](loops/hallmark-design-loop/LOOP.md) | Pages that never look templated. | you request a page | [page](https://gethabit.dev/skills/nutlope/hallmark) |
| [Harness coherence test loop](loops/harness-coherence-test-loop/LOOP.md) | Automation harness stays coherent per PR. | PR changes test harness | [page](https://gethabit.dev/skills/liarjsdev/playwright-stealth-verify) |
| [Harness test loop](loops/harness-test-loop/LOOP.md) | Hooks and skills always tested. | harness files changed | [page](https://gethabit.dev/skills/zernie/test-harness) |
| [Headline snapshot loop](loops/headline-snapshot-loop/LOOP.md) | A daily front-page brief per country. | every morning | [page](https://gethabit.dev/skills/sfkislev/the-news) |
| [HeroUI Native check loop](loops/heroui-native-check-loop/LOOP.md) | HeroUI Native code stays native. | PR changes mobile UI | [page](https://gethabit.dev/skills/heroui-inc/heroui-native) |
| [HF dataset health loop](loops/hf-dataset-health-loop/LOOP.md) | Spot dataset changes every week. | every Monday at nine | [page](https://gethabit.dev/skills/huggingface/huggingface-datasets) |
| [HF fine-tune run loop](loops/hf-finetune-run-loop/LOOP.md) | Fine-tuned models saved to Hub. | training run requested | [page](https://gethabit.dev/skills/huggingface/huggingface-llm-trainer) |
| [Home Assistant review loop](loops/home-assistant-review-loop/LOOP.md) | Automations use native Home Assistant features. | every Sunday evening | [page](https://gethabit.dev/skills/homeassistant-ai/home-assistant-best-practices) |
| [Hook A/B test loop](loops/hook-ab-test-loop/LOOP.md) | Learn which hooks your audience likes. | weekly hook drafting | [page](https://gethabit.dev/skills/blacktwist/hook-writer-sms) |
| [Humanize draft loop](loops/humanize-draft-loop/LOOP.md) | Drafts lose their AI tells. | draft ready for edit | [page](https://gethabit.dev/skills/jpeggdev/humanize-writing) |
| [Root cause hunt loop](loops/hunt-root-cause-loop/LOOP.md) | Find the cause before fixing. | test fails on main | [page](https://gethabit.dev/skills/tw93/hunt) |
| [HyperFrames render loop](loops/hyperframes-render-loop/LOOP.md) | Checked videos, rendered on your OK. | hourly on work days | [page](https://gethabit.dev/skills/heygen-com/hyperframes-cli) |
| [Idea pressure test loop](loops/idea-pressure-test-loop/LOOP.md) | A blunt verdict on every idea. | idea file changes | [page](https://gethabit.dev/skills/buildgreatproducts/idea-validator) |
| [Image batch loop](loops/image-batch-loop/LOOP.md) | Saved prompts become finished images. | new prompt files saved | [page](https://gethabit.dev/skills/jimliu/baoyu-image-gen) |
| [Motion audit plan loop](loops/improve-animations-loop/LOOP.md) | Ranked motion fixes, ready to execute. | monthly motion audit | [page](https://gethabit.dev/skills/emilkowalski/improve-animations) |
| [UI drift audit loop](loops/improve-ui-audit-loop/LOOP.md) | Proven UI fixes, planned for handoff. | biweekly surface audit | [page](https://gethabit.dev/skills/ibelick/improve-ui) |
| [Indexion doc drift loop](loops/indexion-doc-drift-loop/LOOP.md) | Docs keep up with the code. | weekly docs drift check | [page](https://gethabit.dev/skills/trkbt10/indexion-documentation) |
| [Indexion README drift loop](loops/indexion-readme-drift-loop/LOOP.md) | README changes stay purely additive. | docs or package change | [page](https://gethabit.dev/skills/trkbt10/indexion-readme) |
| [InsForge advisor loop](loops/insforge-advisor-loop/LOOP.md) | Clear backend advisor findings weekly. | weekly advisor scan | [page](https://gethabit.dev/skills/insforge/insforge-cli) |
| [InsForge SDK check loop](loops/insforge-sdk-check-loop/LOOP.md) | Catch InsForge SDK mistakes early. | PR touches InsForge code | [page](https://gethabit.dev/skills/insforge/insforge) |
| [Instagram hashtag watch loop](loops/instagram-hashtag-watch-loop/LOOP.md) | Track hashtags and profiles daily. | daily hashtag watch | [page](https://gethabit.dev/skills/fetcher-sh/instagram-api) |
| [Instagram profile watch loop](loops/instagram-profile-watch-loop/LOOP.md) | Fresh public Instagram numbers, logged. | weekly profile check | [page](https://gethabit.dev/skills/skillify-sh/instagram-scraper) |
| [Anti-slop update loop](loops/install-anti-slop-loop/LOOP.md) | Lint rules stay current, customizations kept. | monthly upstream check | [page](https://gethabit.dev/skills/dmmulroy/install-anti-slop) |
| [Interface craft loop](loops/interface-craft-loop/LOOP.md) | Product UI that holds its system. | PR changes product UI | [page](https://gethabit.dev/skills/dammyjay93/interface-design) |
| [Interface review loop](loops/interface-review-loop/LOOP.md) | One ranked verdict across six domains. | weekly flow review | [page](https://gethabit.dev/skills/jakubkrehel/better-interface) |
| [Interrupt safety loop](loops/interrupt-safety-loop/LOOP.md) | Paused graphs resume without duplicates. | PR touches graph code | [page](https://gethabit.dev/skills/langchain-ai/langgraph-human-in-the-loop) |
| [iOS HIG score loop](loops/ios-hig-score-loop/LOOP.md) | Every screen scores toward 10/10. | iOS screen changed | [page](https://gethabit.dev/skills/wondelai/ios-hig-design) |
| [Issue triage loop](loops/issue-triage-loop/LOOP.md) | Sort open issues, act after approval. | untriaged issues pile up | [page](https://gethabit.dev/skills/rtk-ai/issue-triage) |
| [Web extract loop](loops/just-scrape-loop/LOOP.md) | Fresh structured data from web pages. | daily extract run | [page](https://gethabit.dev/skills/scrapegraphai/just-scrape) |
| [KGF spec check loop](loops/kgf-spec-check-loop/LOOP.md) | KGF spec edits keep docs extracted. | KGF spec changes | [page](https://gethabit.dev/skills/trkbt10/indexion-kgf) |
| [Knap notes batch loop](loops/knap-notes-batch-loop/LOOP.md) | Turn new data into notes. | new data file arrives | [page](https://gethabit.dev/skills/kepano/knap) |
| [Knowledge brain refresh loop](loops/knowledge-brain-refresh-loop/LOOP.md) | Keep your work brains current. | every Monday morning | [page](https://gethabit.dev/skills/thedotmack/knowledge-agent) |
| [Knowledge closeout loop](loops/knowledge-closeout-loop/LOOP.md) | Docs, rules and code agree. | change merged | [page](https://gethabit.dev/skills/kkkkhazix/neat-freak) |
| [Landing page audit loop](loops/landing-page-audit-loop/LOOP.md) | Conversion leaks ranked every month. | monthly page audit | [page](https://gethabit.dev/skills/autonnel/landing-page-conversion-audit) |
| [Langfuse trace review loop](loops/langfuse-trace-review-loop/LOOP.md) | Weekly failure modes from real traces. | weekly on Monday | [page](https://gethabit.dev/skills/langfuse/langfuse) |
| [Lark Drive sync loop](loops/lark-drive-sync-loop/LOOP.md) | Local folder matches Drive. | nightly folder sync | [page](https://gethabit.dev/skills/larksuite/lark-drive) |
| [Launch video loop](loops/launch-video-loop/LOOP.md) | A short launch video per release. | new release tag | [page](https://gethabit.dev/skills/latent-spaces/brag) |
| [Layout audit loop](loops/layout-audit-loop/LOOP.md) | Layouts survive resize, translation, RTL. | PR changes styles | [page](https://gethabit.dev/skills/jakubkrehel/better-layout) |
| [Lean PRD loop](loops/lean-prd-loop/LOOP.md) | Every feature idea gets a PRD. | new feature idea filed | [page](https://gethabit.dev/skills/phuryn/create-prd) |
| [Library bundle check loop](loops/library-bundle-check-loop/LOOP.md) | Library builds valid before publish. | pull request opened | [page](https://gethabit.dev/skills/rolldown/tsdown) |
| [Lightweight Charts v5 loop](loops/lightweight-charts-v5-loop/LOOP.md) | Chart code stays on v5. | chart code changes | [page](https://gethabit.dev/skills/tradingview/lightweight-charts) |
| [iOS simulator smoke test loop](loops/limrun-ios-smoke-test-loop/LOOP.md) | Each build gets a smoke test. | iOS build succeeds | [page](https://gethabit.dev/skills/limrun-inc/limrun-ios-simulator) |
| [LinkedIn profile refresh loop](loops/linkedin-profile-refresh-loop/LOOP.md) | Your profile stays search ready. | first day each month | [page](https://gethabit.dev/skills/paramchoudhary/linkedin-profile-optimizer) |
| [LinkedIn weekly content loop](loops/linkedin-weekly-content-loop/LOOP.md) | A week of posts, approved first. | every Monday morning | [page](https://gethabit.dev/skills/sergebulaev/linkedin-marketing) |
| [Pre-commit lint loop](loops/lint-fix-loop/LOOP.md) | Commits that pass lint checks. | before each commit | [page](https://gethabit.dev/skills/react/fix) |
| [Living scope reconcile loop](loops/living-scope-reconcile-loop/LOOP.md) | The scope stays honest after shipping. | a slice ships | [page](https://gethabit.dev/skills/jsmastery-pro/scope) |
| [LLM wiki lint loop](loops/llm-wiki-lint-loop/LOOP.md) | Your wiki stays grounded. | weekly wiki lint | [page](https://gethabit.dev/skills/astro-han/karpathy-llm-wiki) |
| [Logfire coverage loop](loops/logfire-coverage-loop/LOOP.md) | One more service sending real traces. | next service to instrument | [page](https://gethabit.dev/skills/pydantic/logfire-instrumentation) |
| [Logfire error digest loop](loops/logfire-error-digest-loop/LOOP.md) | Daily summary of new errors. | every morning | [page](https://gethabit.dev/skills/pydantic/logfire-query) |
| [Logo animation loop](loops/logo-animation-loop/LOOP.md) | Every logo reveal ships clean. | new logo brief | [page](https://gethabit.dev/skills/iart-ai/logo-animation) |
| [Loki error rate loop](loops/loki-error-rate-loop/LOOP.md) | Log errors spotted every hour. | every hour | [page](https://gethabit.dev/skills/grafana/loki) |
| [Manuscript polish loop](loops/manuscript-polish-loop/LOOP.md) | Tighter prose, same facts. | manuscript section changes | [page](https://gethabit.dev/skills/yuan1z0825/nature-polishing) |
| [marimo notebook check loop](loops/marimo-notebook-check-loop/LOOP.md) | Keep marimo notebooks running clean. | notebook file changes | [page](https://gethabit.dev/skills/marimo-team/marimo-notebook) |
| [Market environment report loop](loops/market-environment-report-loop/LOOP.md) | A daily global market conditions read. | daily market report | [page](https://gethabit.dev/skills/tradermonty/market-environment-analysis) |
| [MD3 compliance audit loop](loops/md3-compliance-audit-loop/LOOP.md) | Your UI stays Material 3 compliant. | UI code changes | [page](https://gethabit.dev/skills/hamen/material-3) |
| [Media gap loop](loops/media-gap-loop/LOOP.md) | Fill media gaps in every video. | video built or reviewed | [page](https://gethabit.dev/skills/heygen-com/media-use) |
| [Mem0 integration loop](loops/mem0-integrate-loop/LOOP.md) | Mem0 added behind a feature flag. | you ask to integrate | [page](https://gethabit.dev/skills/mem0ai/mem0-integrate) |
| [Mem0 verify loop](loops/mem0-verify-loop/LOOP.md) | A Mem0 integration proven to run. | after mem0 integrate | [page](https://gethabit.dev/skills/mem0ai/mem0-test-integration) |
| [Memory recall loop](loops/memory-recall-loop/LOOP.md) | Past context before new work. | you ask about past work | [page](https://gethabit.dev/skills/rohitg00/recall) |
| [Memory save loop](loops/memory-save-loop/LOOP.md) | Every decision saved with tags. | you say remember this | [page](https://gethabit.dev/skills/rohitg00/remember) |
| [Mermaid docs diagram loop](loops/mermaid-docs-diagram-loop/LOOP.md) | Keep diagrams matched to the code. | structure or flow changes | [page](https://gethabit.dev/skills/softaworks/mermaid-diagrams) |
| [Message delivery funnel loop](loops/message-delivery-funnel-loop/LOOP.md) | Delivery drops get caught early. | daily delivery report | [page](https://gethabit.dev/skills/sentdm/messaging-performance-analyzer) |
| [Mintlify docs check loop](loops/mintlify-docs-check-loop/LOOP.md) | Docs pages that validate cleanly. | PR changes docs | [page](https://gethabit.dev/skills/mintlify/mintlify) |
| [Modding field note loop](loops/modding-field-note-loop/LOOP.md) | Every modding session leaves a note. | modding session ends | [page](https://gethabit.dev/skills/rehan-remade/share-field-notes) |
| [MongoDB pool tuning loop](loops/mongodb-pool-tuning-loop/LOOP.md) | Size MongoDB connection pools from evidence. | connection code or errors | [page](https://gethabit.dev/skills/mongodb/mongodb-connection) |
| [MongoDB report query loop](loops/mongodb-report-query-loop/LOOP.md) | Recurring data questions answered read-only. | weekly data questions | [page](https://gethabit.dev/skills/mongodb/mongodb-natural-language-querying) |
| [MongoDB slow query loop](loops/mongodb-slow-query-loop/LOOP.md) | Suggest indexes for slow queries. | weekly slow query review | [page](https://gethabit.dev/skills/mongodb/mongodb-query-optimizer) |
| [Motion audit loop](loops/motion-audit-loop/LOOP.md) | Motion reviewed on every UI change. | PR touches UI motion | [page](https://gethabit.dev/skills/kylezantos/design-motion-principles) |
| [Motion consistency loop](loops/motion-consistency-loop/LOOP.md) | Every shot follows one motion language. | new shot ready | [page](https://gethabit.dev/skills/iart-ai/motion-art-direction) |
| [Motion timing review loop](loops/motion-timing-review-loop/LOOP.md) | Motion never feels stiff again. | animation change submitted | [page](https://gethabit.dev/skills/iart-ai/animation-principles) |
| [MySQL change review loop](loops/mysql-change-review-loop/LOOP.md) | Safe, measured MySQL changes. | PR changes SQL | [page](https://gethabit.dev/skills/planetscale/mysql) |
| [n8n secret audit loop](loops/n8n-secret-audit-loop/LOOP.md) | No secrets hardcoded in workflows. | weekly secret scan | [page](https://gethabit.dev/skills/n8n-io/n8n-credentials-and-security-official) |
| [n8n workflow ship loop](loops/n8n-workflow-ship-loop/LOOP.md) | n8n workflows shipped only after testing. | workflow request arrives | [page](https://gethabit.dev/skills/n8n-io/n8n-workflow-lifecycle-official) |
| [Name drift audit loop](loops/name-drift-audit-loop/LOOP.md) | Names keep matching what code does. | weekly name drift audit | [page](https://gethabit.dev/skills/trkbt10/indexion-identity) |
| [Nano Banana image loop](loops/nanobanana-image-loop/LOOP.md) | Fresh images from every prompt. | new image prompt added | [page](https://gethabit.dev/skills/gargantuax/nanobanana) |
| [Native screen polish loop](loops/native-screen-polish-loop/LOOP.md) | Every mobile screen meets native quality. | screen added or changed | [page](https://gethabit.dev/skills/appllama/appllama-app-design-skill) |
| [Nature figure QA loop](loops/nature-figure-qa-loop/LOOP.md) | Every figure passes QA before delivery. | Figure script changes | [page](https://gethabit.dev/skills/yuan1z0825/nature-figure) |
| [Neon branch per PR loop](loops/neon-branch-per-pr-loop/LOOP.md) | Each PR gets its own database. | pull request opened | [page](https://gethabit.dev/skills/neondatabase/neon-postgres-branches) |
| [Neon function deploy check loop](loops/neon-function-deploy-check-loop/LOOP.md) | Functions deploy locked down. | function code changed | [page](https://gethabit.dev/skills/neondatabase/neon-functions) |
| [Postgres health loop](loops/neon-postgres-loop/LOOP.md) | Slow queries found and verified. | weekly health check | [page](https://gethabit.dev/skills/neondatabase/neon-postgres) |
| [Netlify config review loop](loops/netlify-config-review-loop/LOOP.md) | Netlify config changes ship without surprises. | netlify config changes | [page](https://gethabit.dev/skills/netlify/netlify-config) |
| [Netlify edge function check loop](loops/netlify-edge-function-check-loop/LOOP.md) | No silent edge functions ship. | edge function file changed | [page](https://gethabit.dev/skills/netlify/netlify-edge-functions) |
| [Netlify forms check loop](loops/netlify-forms-check-loop/LOOP.md) | Every form still gets submissions. | form markup changed | [page](https://gethabit.dev/skills/netlify/netlify-forms) |
| [Next instant route loop](loops/next-instant-route-loop/LOOP.md) | One more route paints instantly. | route picked for optimizing | [page](https://gethabit.dev/skills/vercel/next-cache-components-optimizer) |
| [Next.js cache audit loop](loops/nextjs-cache-audit-loop/LOOP.md) | Cache tags and invalidation stay correct. | data or action change | [page](https://gethabit.dev/skills/mohamed-hossam1/nextjs-cache-architecture) |
| [Next.js SEO audit loop](loops/nextjs-seo-audit-loop/LOOP.md) | Next.js pages stay indexable. | weekly SEO audit | [page](https://gethabit.dev/skills/laguagu/nextjs-seo) |
| [no-mistakes gate loop](loops/no-mistakes-gate-loop/LOOP.md) | Ship branches only through the gate. | task committed on branch | [page](https://gethabit.dev/skills/kunchenguid/no-mistakes) |
| [Node.js core commit loop](loops/nodejs-core-commit-loop/LOOP.md) | Commits that pass CI first. | before each commit | [page](https://gethabit.dev/skills/mcollina/nodejs-core) |
| [NotebookLM briefing loop](loops/notebooklm-briefing-loop/LOOP.md) | Weekly sources become one briefing. | weekly source briefing | [page](https://gethabit.dev/skills/teng-lin/notebooklm) |
| [Nx generate verify loop](loops/nx-generate-verify-loop/LOOP.md) | Scaffolded code that passes checks. | you ask to scaffold | [page](https://gethabit.dev/skills/nrwl/nx-generate) |
| [Nx workspace map loop](loops/nx-workspace-map-loop/LOOP.md) | A current map of your monorepo. | every Monday | [page](https://gethabit.dev/skills/nrwl/nx-workspace) |
| [Object storage setup loop](loops/object-storage-setup-loop/LOOP.md) | File uploads keep working. | backend or frontend changed | [page](https://gethabit.dev/skills/caffeinelabs/extension-object-storage) |
| [Obsidian note tidy loop](loops/obsidian-note-tidy-loop/LOOP.md) | New notes use clean Obsidian syntax. | evening note check | [page](https://gethabit.dev/skills/kepano/obsidian-markdown) |
| [Obsidian vault CLI loop](loops/obsidian-vault-cli-loop/LOOP.md) | Notes managed without opening Obsidian. | You ask for note task | [page](https://gethabit.dev/skills/hkuds/cli-anything-obsidian) |
| [OCR delegated review loop](loops/ocr-delegated-review-loop/LOOP.md) | Review every changed file, report coverage. | pull request opened | [page](https://gethabit.dev/skills/alibaba/open-code-review-delegate) |
| [OKF bundle upkeep loop](loops/okf-bundle-upkeep-loop/LOOP.md) | Knowledge bundle stays conformant. | weekly bundle check | [page](https://gethabit.dev/skills/inkeep/okf-knowledge-base) |
| [OKX bot watch loop](loops/okx-bot-watch-loop/LOOP.md) | Your OKX bots, checked daily. | every morning | [page](https://gethabit.dev/skills/okx/okx-cex-bot) |
| [OKX market snapshot loop](loops/okx-market-snapshot-loop/LOOP.md) | Log a daily market snapshot. | every morning | [page](https://gethabit.dev/skills/okx/okx-cex-market) |
| [OKX portfolio snapshot loop](loops/okx-portfolio-snapshot-loop/LOOP.md) | Know your exchange balances daily. | every morning at seven | [page](https://gethabit.dev/skills/okx/okx-cex-portfolio) |
| [OKX skill verify loop](loops/okx-skill-verify-loop/LOOP.md) | Installed skills stay verified. | weekly skill check | [page](https://gethabit.dev/skills/okx/okx-cex-skill-mp) |
| [Onboarding guide refresh loop](loops/onboarding-guide-refresh-loop/LOOP.md) | Onboarding guide matches the code. | graph refreshed | [page](https://gethabit.dev/skills/egonex-ai/understand-onboard) |
| [OpenAI Agents SDK test loop](loops/openai-agents-test-loop/LOOP.md) | Agent changes verified offline first. | agents code changes | [page](https://gethabit.dev/skills/laguagu/openai-agents-sdk) |
| [OpenCLI adapter repair loop](loops/opencli-adapter-repair-loop/LOOP.md) | Broken site adapters get fixed fast. | nightly adapter test | [page](https://gethabit.dev/skills/jackwener/opencli-adapter-author) |
| [OpenCLI autofix loop](loops/opencli-autofix-loop/LOOP.md) | Broken adapters fixed and retried. | opencli command fails | [page](https://gethabit.dev/skills/jackwener/opencli-autofix) |
| [OpenCLI topic watch loop](loops/opencli-topic-watch-loop/LOOP.md) | A fresh topic digest, sources logged. | every morning | [page](https://gethabit.dev/skills/jackwener/smart-search) |
| [OpenSpec bulk archive loop](loops/openspec-bulk-archive-loop/LOOP.md) | Clear finished changes in batches. | end of sprint | [page](https://gethabit.dev/skills/fission-ai/openspec-bulk-archive-change) |
| [OpenTelemetry pipeline check loop](loops/otel-pipeline-check-loop/LOOP.md) | Know telemetry still reaches Grafana. | daily telemetry check | [page](https://gethabit.dev/skills/grafana/opentelemetry) |
| [OWASP PR audit loop](loops/owasp-pr-audit-loop/LOOP.md) | Security flaws caught before deploy. | pull request opened | [page](https://gethabit.dev/skills/sergiodxa/owasp-security-check) |
| [Page change archive loop](loops/page-change-archive-loop/LOOP.md) | Watched page changes preserved as evidence. | weekly archive check | [page](https://gethabit.dev/skills/useosint/read-deleted-pages) |
| [Page metadata audit loop](loops/page-metadata-audit-loop/LOOP.md) | Every new page ships correct metadata. | PR changes pages | [page](https://gethabit.dev/skills/ibelick/fixing-metadata) |
| [Page watch extract loop](loops/page-watch-extract-loop/LOOP.md) | Know when watched pages change. | every Monday morning | [page](https://gethabit.dev/skills/parallel-web/parallel-web-extract) |
| [Paper citation check loop](loops/paper-citation-check-loop/LOOP.md) | No unverified citation reaches submission. | push to paper repo | [page](https://gethabit.dev/skills/orchestra-research/ml-paper-writing) |
| [Paper figure refresh loop](loops/paper-figure-refresh-loop/LOOP.md) | Paper figures rebuilt from latest results. | results file changes | [page](https://gethabit.dev/skills/orchestra-research/academic-plotting) |
| [Paper section revision loop](loops/paper-section-revision-loop/LOOP.md) | One paper section clearer each pass. | next section to revise | [page](https://gethabit.dev/skills/master-cai/research-paper-writing) |
| [Paperclip design guide sync loop](loops/paperclip-design-guide-sync-loop/LOOP.md) | Keep components and design guide synced. | UI components change | [page](https://gethabit.dev/skills/paperclipai/design-guide) |
| [Paperclip hire loop](loops/paperclip-hire-loop/LOOP.md) | A reviewed hire request, submitted. | hire task assigned | [page](https://gethabit.dev/skills/paperclipai/paperclip-create-agent) |
| [Paperclip plugin loop](loops/paperclip-plugin-loop/LOOP.md) | Plugin builds, tests and installs. | plugin code changed | [page](https://gethabit.dev/skills/paperclipai/paperclip-create-plugin) |
| [PARA memory weekly loop](loops/para-memory-weekly-loop/LOOP.md) | Keep agent memory sorted weekly. | weekly memory synthesis | [page](https://gethabit.dev/skills/paperclipai/para-memory-files) |
| [Parallel web search loop](loops/parallel-web-search-loop/LOOP.md) | Cited web answers every morning. | every weekday morning | [page](https://gethabit.dev/skills/parallel-web/parallel-web-search) |
| [Payload translations loop](loops/payload-translations-loop/LOOP.md) | Every new key gets translated. | English keys change | [page](https://gethabit.dev/skills/payloadcms/generate-translations) |
| [PDF text extract loop](loops/pdf-text-extract-loop/LOOP.md) | New PDFs turned into usable text. | new PDF added | [page](https://gethabit.dev/skills/shareai-lab/pdf) |
| [Personal assistant brief loop](loops/personal-assistant-brief-loop/LOOP.md) | A daily plan from your profile. | every weekday morning | [page](https://gethabit.dev/skills/ailabs-393/personal-assistant) |
| [Perspective refresh loop](loops/perspective-refresh-loop/LOOP.md) | Perspective skills stay current. | monthly perspective refresh | [page](https://gethabit.dev/skills/alchaincyf/huashu-nuwa) |
| [PHP audit loop](loops/php-audit-loop/LOOP.md) | PHP code checked against modern rules. | PHP code changes | [page](https://gethabit.dev/skills/asyrafhussin/php-best-practices) |
| [Pipeline coverage weekly loop](loops/pipeline-coverage-weekly-loop/LOOP.md) | Coverage gaps caught by week six. | Mondays at 08:00 | [page](https://gethabit.dev/skills/mbfinotti/sales-pipeline-coverage-modeling) |
| [Plan crafting loop](loops/plan-crafting-loop/LOOP.md) | Approved specs become executable plans. | spec approved | [page](https://gethabit.dev/skills/sentimony/plan-crafting) |
| [Plan file tick loop](loops/plan-file-tick-loop/LOOP.md) | Long tasks finish, nothing forgotten. | every 10 minutes | [page](https://gethabit.dev/skills/othmanadi/planning-with-files) |
| [Plan grill loop](loops/plan-grill-loop/LOOP.md) | Turn every idea into tickets. | issue labelled idea | [page](https://gethabit.dev/loops/plan-grill-loop) |
| [PlanetScale feature gap loop](loops/planetscale-feature-gap-loop/LOOP.md) | Find missing database safety features. | quarterly database review | [page](https://gethabit.dev/skills/planetscale/planetscale-best-practices-matrix) |
| [PlanetScale recommendation loop](loops/planetscale-recommendation-loop/LOOP.md) | Schema fixes proposed, never auto-deployed. | daily recommendation sweep | [page](https://gethabit.dev/skills/planetscale/planetscale-mcp-agent-operating-model) |
| [Planning with files loop](loops/planning-with-files-zht-loop/LOOP.md) | Long tasks survive every restart. | new multi-step task | [page](https://gethabit.dev/skills/othmanadi/planning-with-files-zht) |
| [Plan denial review loop](loops/plannotator-compound-loop/LOOP.md) | Fewer denied plans each month. | first day each month | [page](https://gethabit.dev/skills/backnotprop/plannotator-compound) |
| [Playwright E2E and links loop](loops/playwright-e2e-links-loop/LOOP.md) | No broken flows or dead links. | push to main | [page](https://gethabit.dev/skills/alinaqi/playwright-testing) |
| [Playwright site check loop](loops/playwright-site-check-loop/LOOP.md) | Catch broken pages every night. | nightly browser check | [page](https://gethabit.dev/skills/lackeyjb/playwright-skill) |
| [Playwright suite gate loop](loops/playwright-suite-gate-loop/LOOP.md) | E2E tests that stay stable. | PR changes e2e tests | [page](https://gethabit.dev/skills/petrkindlmann/playwright-automation) |
| [Plugin docs sync loop](loops/plugin-docs-sync-loop/LOOP.md) | Plugin docs match the marketplace. | marketplace.json changes | [page](https://gethabit.dev/skills/geoffjay/documentation-update) |
| [Podcast transcript loop](loops/podcast-transcript-loop/LOOP.md) | New episodes transcribed on their own. | daily feed check | [page](https://gethabit.dev/skills/theplasmak/faster-whisper) |
| [Ponytail PR review loop](loops/ponytail-review-loop/LOOP.md) | Every change reviewed before merge. | pull request opened | [page](https://gethabit.dev/skills/dietrichgebert/ponytail-review) |
| [Postgres safety review loop](loops/postgres-safety-review-loop/LOOP.md) | Postgres safety gaps found, nothing changed. | monthly safety review | [page](https://gethabit.dev/skills/planetscale/planetscale-postgres-safety-review) |
| [PR review JSON loop](loops/pr-review-json-loop/LOOP.md) | Every PR gets a validated review. | pull request opened | [page](https://gethabit.dev/skills/warpdotdev/review-pr) |
| [PRD review loop](loops/prd-review-loop/LOOP.md) | Short PRDs with clear problems. | new PRD draft | [page](https://gethabit.dev/skills/refoundai/writing-prds) |
| [PRD to tasks loop](loops/prd-to-tasks-loop/LOOP.md) | Ideas become PRDs and tasks. | you describe an idea | [page](https://gethabit.dev/skills/pageai-pro/prd-creator) |
| [Pre-mortem loop](loops/pre-mortem-loop/LOOP.md) | Catch launch risks while fixable. | launch plan changed | [page](https://gethabit.dev/skills/phuryn/pre-mortem) |
| [Printing Press reprint loop](loops/printing-press-reprint-loop/LOOP.md) | Regenerate CLIs after machine upgrades. | Printing Press upgrade lands | [page](https://gethabit.dev/skills/mvanhorn/printing-press-reprint) |
| [Prisma adapter check loop](loops/prisma-adapter-check-loop/LOOP.md) | Driver adapter changes pass the checklist. | PR touches adapter code | [page](https://gethabit.dev/skills/prisma/prisma-driver-adapter-implementation) |
| [Prisma schema check loop](loops/prisma-schema-check-loop/LOOP.md) | Schema valid, migrations in sync. | schema file changed | [page](https://gethabit.dev/skills/prisma/prisma-cli) |
| [Product spec loop](loops/product-spec-loop/LOOP.md) | Behavior written as testable invariants. | feature needs a spec | [page](https://gethabit.dev/skills/warpdotdev/write-product-spec) |
| [Product video record loop](loops/product-video-record-loop/LOOP.md) | Narrated product videos kept current. | product UI changes | [page](https://gethabit.dev/skills/screenci/screenci) |
| [Product Hunt watch loop](loops/producthunt-watch-loop/LOOP.md) | Daily digest of new launches. | every morning | [page](https://gethabit.dev/skills/resciencelab/producthunt) |
| [Programmatic SEO quality loop](loops/programmatic-seo-quality-loop/LOOP.md) | Template pages stay unique and indexable. | page data changed | [page](https://gethabit.dev/skills/coreyhaines31/programmatic-seo) |
| [Prose clarity edit loop](loops/prose-clarity-edit-loop/LOOP.md) | Human-facing prose reads clear and tight. | prose files change | [page](https://gethabit.dev/skills/softaworks/writing-clearly-and-concisely) |
| [Public page scrape loop](loops/public-page-scrape-loop/LOOP.md) | Collect public pages, stop at blocks. | daily source collection | [page](https://gethabit.dev/skills/jamditis/web-scraping) |
| [PUDL schema watch loop](loops/pudl-schema-watch-loop/LOOP.md) | Know when your PUDL tables change. | weekly descriptor check | [page](https://gethabit.dev/skills/catalyst-cooperative/pudl) |
| [Pydantic AI agent test loop](loops/pydantic-ai-agent-test-loop/LOOP.md) | Keep Pydantic AI agents tested, traced. | agent code changes | [page](https://gethabit.dev/skills/pydantic/building-pydantic-ai-agents) |
| [Pydantic model review loop](loops/pydantic-model-review-loop/LOOP.md) | Pydantic models use built-in validation. | model files changed | [page](https://gethabit.dev/skills/pydantic/pydantic) |
| [QMD notes index loop](loops/qmd-notes-index-loop/LOOP.md) | Keep your markdown notes searchable. | nightly index refresh | [page](https://gethabit.dev/skills/tobi/qmd) |
| [Qodo rules loop](loops/qodo-rules-loop/LOOP.md) | Team coding rules applied every task. | coding task starts | [page](https://gethabit.dev/skills/qodo-ai/qodo-get-rules) |
| [QQ Music weekly report loop](loops/qqmusic-weekly-report-loop/LOOP.md) | Weekly listening report, plus version check. | weekly on Sunday | [page](https://gethabit.dev/skills/tencentmusic/qqmusic) |
| [Query insights review loop](loops/query-insights-review-loop/LOOP.md) | Weekly risky queries and tag gaps. | weekly insights review | [page](https://gethabit.dev/skills/planetscale/planetscale-query-insights-and-tags) |
| [R8 keep rules audit loop](loops/r8-keep-rules-audit-loop/LOOP.md) | Leaner, non-redundant R8 keep rules. | you ask for R8 audit | [page](https://gethabit.dev/skills/android/r8-analyzer) |
| [Radix to Base UI loop](loops/radix-to-base-migration-loop/LOOP.md) | One component migrated per run. | daily migration step | [page](https://gethabit.dev/skills/shadcn-ui/migrate-radix-to-base) |
| [Ralph PRD convert loop](loops/ralph-prd-convert-loop/LOOP.md) | Every PRD becomes runnable stories. | new PRD file added | [page](https://gethabit.dev/skills/snarktank/ralph) |
| [React channel test loop](loops/react-channel-test-loop/LOOP.md) | React tests run per channel. | React core pull request | [page](https://gethabit.dev/skills/react/test) |
| [React component review loop](loops/react-component-review-loop/LOOP.md) | React changes reviewed before merge. | React files change | [page](https://gethabit.dev/skills/giuseppe-trisciuoglio/react-code-review) |
| [React Email template loop](loops/react-email-template-loop/LOOP.md) | Email templates render in every inbox. | emails folder changes | [page](https://gethabit.dev/skills/resend/react-email) |
| [React error codes loop](loops/react-error-codes-loop/LOOP.md) | Every new error gets a code. | pull request opened | [page](https://gethabit.dev/skills/react/extract-errors) |
| [React feature flags loop](loops/react-feature-flags-loop/LOOP.md) | Flags consistent across every fork. | flag files change | [page](https://gethabit.dev/skills/react/feature-flags) |
| [Flow type check loop](loops/react-flow-check-loop/LOOP.md) | No Flow errors reach main. | pull request updated | [page](https://gethabit.dev/skills/react/flow) |
| [React Native perf sweep loop](loops/react-native-perf-sweep-loop/LOOP.md) | The app gets measurably faster. | weekly performance sweep | [page](https://gethabit.dev/skills/software-mansion/argent-react-native-optimization) |
| [React Native profile trend loop](loops/react-native-profile-trend-loop/LOOP.md) | Render regressions show up early. | weekly profiling run | [page](https://gethabit.dev/skills/software-mansion/argent-react-native-profiler) |
| [React Native run check loop](loops/react-native-run-check-loop/LOOP.md) | The app builds and runs clean. | app code changed | [page](https://gethabit.dev/skills/software-mansion/argent-react-native-app-workflow) |
| [React Router bug fix loop](loops/react-router-bug-fix-loop/LOOP.md) | Fix reported bugs with tests. | you pass an issue | [page](https://gethabit.dev/skills/remix-run/fix-bug) |
| [React Router mode check loop](loops/react-router-mode-check-loop/LOOP.md) | Route changes match the app's mode. | route code changes | [page](https://gethabit.dev/skills/remix-run/react-router) |
| [Read loop](loops/read-loop/LOOP.md) | Fresh summaries of saved links. | every Monday morning | [page](https://gethabit.dev/skills/tw93/read) |
| [Red green loop](loops/red-green-loop/LOOP.md) | Features built test-first, slice by slice. | you start a feature | [page](https://gethabit.dev/skills/mattpocock/tdd) |
| [Reddit leads loop](loops/reddit-leads-loop/LOOP.md) | Fresh scored Reddit leads daily. | every morning | [page](https://gethabit.dev/skills/lignertys/reddit-leads) |
| [Reddit pain point loop](loops/reddit-pain-point-loop/LOOP.md) | Reddit pain points, every week. | weekly Monday research run | [page](https://gethabit.dev/skills/lignertys/reddit-research) |
| [Reddit pulse loop](loops/reddit-pulse-loop/LOOP.md) | Weekly Reddit signals on your topics. | every Monday morning | [page](https://gethabit.dev/skills/lignertys/reddapi) |
| [Reddit subreddit watch loop](loops/reddit-subreddit-watch-loop/LOOP.md) | A daily pull of subreddit activity. | daily subreddit check | [page](https://gethabit.dev/skills/resciencelab/reddit) |
| [Redis client review loop](loops/redis-client-review-loop/LOOP.md) | Redis clients stay pooled and fast. | PR touches Redis code | [page](https://gethabit.dev/skills/redis/redis-connections) |
| [Redis hardening loop](loops/redis-hardening-loop/LOOP.md) | Redis stays locked down. | weekly Redis audit | [page](https://gethabit.dev/skills/redis/redis-security) |
| [Redis health check loop](loops/redis-health-check-loop/LOOP.md) | Catch Redis trouble before users do. | hourly health check | [page](https://gethabit.dev/skills/redis/redis-observability) |
| [Refero design loop](loops/refero-design-loop/LOOP.md) | Designs grounded in real references. | issue labelled design | [page](https://gethabit.dev/skills/referodesign/refero-design) |
| [Regression suite refresh loop](loops/regression-suite-refresh-loop/LOOP.md) | Regression suite tracks new features. | feature shipped | [page](https://gethabit.dev/skills/softaworks/qa-test-planner) |
| [Replay scanner sizing loop](loops/replay-scanner-sizing-loop/LOOP.md) | Scanners sized before they run. | scanner create or widen | [page](https://gethabit.dev/skills/posthog/creating-replay-vision-scanners) |
| [Replicate batch run loop](loops/replicate-batch-run-loop/LOOP.md) | Queued generations done and saved. | hourly job queue | [page](https://gethabit.dev/skills/replicate/run-models) |
| [Replicate model bake-off loop](loops/replicate-model-bakeoff-loop/LOOP.md) | Your model choice re-tested each month. | monthly model bake-off | [page](https://gethabit.dev/skills/replicate/compare-models) |
| [Replicate model shortlist loop](loops/replicate-model-shortlist-loop/LOOP.md) | Your model shortlist stays current. | weekly model check | [page](https://gethabit.dev/skills/replicate/find-models) |
| [Fresh reviewer loop](loops/requesting-code-review-loop/LOOP.md) | Every task reviewed before merge. | task done or merge | [page](https://gethabit.dev/skills/obra/requesting-code-review) |
| [Research candidate loop](loops/research-explore-loop/LOOP.md) | One ranked research candidate per run. | you authorize exploration | [page](https://gethabit.dev/skills/lllllllama/ai-research-explore) |
| [Resend health check loop](loops/resend-cli-loop/LOOP.md) | Catch Resend setup problems early. | daily Resend check | [page](https://gethabit.dev/skills/resend/resend-cli) |
| [Resume tailor loop](loops/resume-tailor-loop/LOOP.md) | A truthful resume per posting. | new job posting added | [page](https://gethabit.dev/skills/paramchoudhary/resume-tailor) |
| [Motion review loop](loops/review-animations-loop/LOOP.md) | Every animation earns its place. | PR changes motion code | [page](https://gethabit.dev/skills/emilkowalski/review-animations) |
| [RNTL component test loop](loops/rntl-component-test-loop/LOOP.md) | Keep React Native components covered. | a component changes | [page](https://gethabit.dev/skills/callstack/react-native-testing) |
| [Rsbuild config review loop](loops/rsbuild-config-review-loop/LOOP.md) | Rsbuild builds stay lean and safe. | PR changes build config | [page](https://gethabit.dev/skills/rstackjs/rsbuild-best-practices) |
| [RTK cross triage loop](loops/rtk-cross-triage-loop/LOOP.md) | Weekly cross-check of issues and PRs. | weekly triage | [page](https://gethabit.dev/skills/rtk-ai/rtk-triage) |
| [RTK filter TDD loop](loops/rtk-filter-tdd-loop/LOOP.md) | Every new filter proves its savings. | new filter requested | [page](https://gethabit.dev/skills/rtk-ai/tdd-rust) |
| [Runbook check loop](loops/runbook-check-loop/LOOP.md) | Runbooks stay runnable and honest. | runbook pull request | [page](https://gethabit.dev/skills/riekelt/writing-runbooks) |
| [Runpod inventory loop](loops/runpod-inventory-loop/LOOP.md) | Weekly Runpod inventory, nothing touched. | every Monday morning | [page](https://gethabit.dev/skills/runpod/runpod-mcp) |
| [Rust CI fix loop](loops/rust-ci-fix-loop/LOOP.md) | Red builds turned green, narrowly. | CI check fails | [page](https://gethabit.dev/skills/warpdotdev/fix-errors) |
| [Rust correctness review loop](loops/rust-correctness-review-loop/LOOP.md) | Changes that crash, never corrupt. | Rust code changes | [page](https://gethabit.dev/skills/tursodatabase/code-quality) |
| [Rust guidelines review loop](loops/rust-guidelines-review-loop/LOOP.md) | Keep Rust code idiomatic and safe. | Rust pull request opened | [page](https://gethabit.dev/skills/leonardomso/rust-skills) |
| [Rust TDD gate loop](loops/rust-tdd-gate-loop/LOOP.md) | Every Rust change starts red. | Rust task starts | [page](https://gethabit.dev/skills/rtk-ai/rtk-tdd) |
| [Sales career check-in loop](loops/sales-career-checkin-loop/LOOP.md) | Your career plan stays on track. | Sundays at 18:00 | [page](https://gethabit.dev/skills/mbfinotti/sales-career) |
| [Sanity migration rerun loop](loops/sanity-migration-rerun-loop/LOOP.md) | Migration reruns converge, checks pass. | Nightly during migration | [page](https://gethabit.dev/skills/sanity-io/sanity-migration) |
| [Sanity review loop](loops/sanity-review-loop/LOOP.md) | Sanity changes follow house rules. | PR touches Sanity code | [page](https://gethabit.dev/skills/sanity-io/sanity-best-practices) |
| [Scaffold upgrade loop](loops/scaffold-upgrade-loop/LOOP.md) | Agent projects stay on current templates. | monthly template upgrade | [page](https://gethabit.dev/skills/google/google-agents-cli-scaffold) |
| [Schema review loop](loops/schema-review-loop/LOOP.md) | Schema changes pass the design checklist. | schema or migration change | [page](https://gethabit.dev/skills/softaworks/database-schema-designer) |
| [Scope triage loop](loops/scope-triage-loop/LOOP.md) | Every request gets a route first. | new request arrives | [page](https://gethabit.dev/skills/sentimony/scope-triage) |
| [SendCutSend preflight loop](loops/sendcutsend-preflight-loop/LOOP.md) | Every part file gets preflighted. | DXF or STEP changed | [page](https://gethabit.dev/skills/earthtojake/sendcutsend) |
| [SEO and AEO audit loop](loops/seo-aeo-audit-loop/LOOP.md) | Keep pages ready for search. | weekly page check | [page](https://gethabit.dev/skills/sanity-io/seo-aeo-best-practices) |
| [Monthly SEO audit loop](loops/seo-audit-loop/LOOP.md) | SEO issues found and ranked. | first of the month | [page](https://gethabit.dev/skills/coreyhaines31/seo-audit) |
| [SEO content audit loop](loops/seo-content-audit-loop/LOOP.md) | Weekly content quality scores. | every Monday morning | [page](https://gethabit.dev/skills/agricidaniel/seo-content) |
| [SEO drift audit loop](loops/seo-drift-audit-loop/LOOP.md) | Catch SEO drops every week. | every Monday morning | [page](https://gethabit.dev/skills/agricidaniel/seo) |
| [SEO GEO audit loop](loops/seo-geo-audit-loop/LOOP.md) | Site stays findable by AI search. | weekly site audit | [page](https://gethabit.dev/skills/resciencelab/seo-geo) |
| [SEO loop](loops/seo-loop/LOOP.md) | Rank new pages every 21 days. | every 21 days | [page](https://gethabit.dev/loops/seo-loop) |
| [SERP rank track loop](loops/serp-rank-track-loop/LOOP.md) | A daily record of search ranks. | daily rank check | [page](https://gethabit.dev/skills/fetcher-sh/google-search) |
| [SERP rank watch loop](loops/serp-rank-watch-loop/LOOP.md) | Weekly search ranks for your keywords. | weekly rank check | [page](https://gethabit.dev/skills/brightdata/bright-data-best-practices) |
| [SERP snapshot loop](loops/serp-snapshot-loop/LOOP.md) | Weekly search results saved per keyword. | weekly SERP snapshot | [page](https://gethabit.dev/skills/brightdata/brightdata-cli) |
| [Session handoff loop](loops/session-handoff-loop/LOOP.md) | Every session ends with a handoff. | session ends | [page](https://gethabit.dev/skills/mattpocock/handoff) |
| [Session history loop](loops/session-history-loop/LOOP.md) | See past sessions every week. | every Monday morning | [page](https://gethabit.dev/skills/rohitg00/session-history) |
| [shadcn component check loop](loops/shadcn-component-check-loop/LOOP.md) | New UI components ship type-safe. | PR changes components/ui | [page](https://gethabit.dev/skills/google-labs-code/shadcn-ui) |
| [shadcn-svelte update loop](loops/shadcn-svelte-update-loop/LOOP.md) | Keep Svelte UI components current. | monthly component update | [page](https://gethabit.dev/skills/huntabyte/shadcn-svelte) |
| [shadcn upstream sync loop](loops/shadcn-upstream-sync-loop/LOOP.md) | Components current, local changes kept. | weekly component sync | [page](https://gethabit.dev/skills/shadcn-ui/shadcn) |
| [Short story draft loop](loops/short-story-draft-loop/LOOP.md) | Short stories from emotion to draft. | author starts a story | [page](https://gethabit.dev/skills/zenstory-ai/story-short-write) |
| [Shortcut debt ledger loop](loops/shortcut-debt-ledger-loop/LOOP.md) | No shortcut quietly becomes permanent. | weekly debt scan | [page](https://gethabit.dev/skills/dietrichgebert/ponytail-debt) |
| [Sigma spaced review loop](loops/sigma-spaced-review-loop/LOOP.md) | Learned concepts stay learned. | daily review session | [page](https://gethabit.dev/skills/sanyuan0704/sigma) |
| [Simple English docs loop](loops/simple-english-docs-loop/LOOP.md) | Every doc reads plain English. | docs change in PR | [page](https://gethabit.dev/skills/aminblg/simple-english) |
| [Skill review loop](loops/skill-review-loop/LOOP.md) | Every skill change gets reviewed. | SKILL.md changed | [page](https://gethabit.dev/skills/sanyuan0704/skill-review) |
| [Skill security audit loop](loops/skill-security-audit-loop/LOOP.md) | Vet every new skill first. | new skill added | [page](https://gethabit.dev/skills/superagent-ai/skill-security) |
| [Skill size loop](loops/skill-size-loop/LOOP.md) | Your skills stay short and loadable. | a SKILL.md changes | [page](https://gethabit.dev/skills/siviter-xyz/create-skill) |
| [Skill vetting loop](loops/skill-vetting-loop/LOOP.md) | Every skill vetted before install. | Skill install or update | [page](https://gethabit.dev/skills/useai-pro/skill-vetter) |
| [Slack API call audit loop](loops/slack-api-call-audit-loop/LOOP.md) | Slack API calls stay correct. | PR changes Slack calls | [page](https://gethabit.dev/skills/slackapi/slack-api) |
| [Slack changelog watch loop](loops/slack-changelog-watch-loop/LOOP.md) | Slack platform changes never surprise you. | every Monday | [page](https://gethabit.dev/skills/slackapi/slack-docs) |
| [Slack decision digest loop](loops/slack-decision-digest-loop/LOOP.md) | Weekly decisions found and summarised. | every Friday | [page](https://gethabit.dev/skills/slackapi/slack-search) |
| [Social photo set loop](loops/social-photo-set-loop/LOOP.md) | On-brand social images for each campaign. | new campaign brief | [page](https://gethabit.dev/skills/nextlevelbuilder/design) |
| [Session handoff loop](loops/softaworks-session-handoff-loop/LOOP.md) | Fresh agents resume with full context. | session ends or fills | [page](https://gethabit.dev/skills/softaworks/session-handoff) |
| [Solana program check loop](loops/solana-program-check-loop/LOOP.md) | Solana changes built, tested, risk-noted. | PR changes Solana code | [page](https://gethabit.dev/skills/solana-foundation/solana-dev) |
| [Sound effects loop](loops/sound-effects-loop/LOOP.md) | Every listed sound gets generated. | new sound request listed | [page](https://gethabit.dev/skills/elevenlabs/sound-effects) |
| [Spec design loop](loops/spec-design-loop/LOOP.md) | Each feature gets an approved spec. | you start a feature | [page](https://gethabit.dev/skills/klerith/spec) |
| [Spec drift gate loop](loops/spec-drift-gate-loop/LOOP.md) | Implementation stays aligned with the spec. | pull request opened | [page](https://gethabit.dev/skills/trkbt10/indexion-sdd) |
| [Spec first loop](loops/spec-first-loop/LOOP.md) | No code before an approved spec. | new feature request | [page](https://gethabit.dev/skills/addyosmani/spec-driven-development) |
| [Spec gated build loop](loops/spec-gated-build-loop/LOOP.md) | Features built only from settled specs. | you start a build | [page](https://gethabit.dev/skills/jsmastery-pro/develop) |
| [Spec implement loop](loops/spec-implement-loop/LOOP.md) | Approved specs implemented on their branch. | you implement a spec | [page](https://gethabit.dev/skills/klerith/spec-impl) |
| [Spending insights loop](loops/spending-insights-loop/LOOP.md) | A weekly answer about your spending. | every Monday morning | [page](https://gethabit.dev/skills/stripe/financial-insights) |
| [Sqltest conversion loop](loops/sqltest-conversion-loop/LOOP.md) | Legacy TCL tests move to sqltest. | nightly test conversion | [page](https://gethabit.dev/skills/tursodatabase/testing) |
| [Site audit fix loop](loops/squirrel-site-audit-loop/LOOP.md) | Site score climbs every week. | weekly or audit event | [page](https://gethabit.dev/skills/squirrelscan/audit-website) |
| [STE plain text loop](loops/ste-plain-text-loop/LOOP.md) | Keep agent-facing text unambiguous. | agent-facing text changes | [page](https://gethabit.dev/skills/danyuchn/asd-ste100) |
| [Stop slop draft loop](loops/stop-slop-draft-loop/LOOP.md) | Drafts ship without AI tells. | new draft committed | [page](https://gethabit.dev/skills/hardikpandya/stop-slop) |
| [Store screenshots refresh loop](loops/store-screenshots-refresh-loop/LOOP.md) | Store screenshots that sell features. | new app captures added | [page](https://gethabit.dev/skills/parthjadhav/app-store-screenshots) |
| [Strategy red-team loop](loops/strategy-red-team-loop/LOOP.md) | Every plan gets attacked first. | plan document changed | [page](https://gethabit.dev/skills/phuryn/strategy-red-team) |
| [Strix fix and verify loop](loops/strix-fix-verify-loop/LOOP.md) | Findings fixed and proven closed. | Strix scan reports findings | [page](https://gethabit.dev/skills/usestrix/fix-security-vulnerabilities-with-strix) |
| [Studio test coverage loop](loops/studio-test-coverage-loop/LOOP.md) | Every Studio change gets right tests. | Studio code changes | [page](https://gethabit.dev/skills/supabase/studio-testing) |
| [Study quiz loop](loops/study-quiz-loop/LOOP.md) | Find and fix your blind spots. | daily study session | [page](https://gethabit.dev/skills/bevibing/tutor) |
| [StudyVault build loop](loops/studyvault-build-loop/LOOP.md) | Sources turned into a study vault. | new sources added | [page](https://gethabit.dev/skills/bevibing/tutor-setup) |
| [Supabase schema guard loop](loops/supabase-schema-guard-loop/LOOP.md) | Safe schema changes, checked migrations. | schema change in PR | [page](https://gethabit.dev/skills/supabase/supabase) |
| [Supabase server auth review loop](loops/supabase-server-auth-review-loop/LOOP.md) | Edge Function auth stays correct. | edge function changes | [page](https://gethabit.dev/skills/supabase/supabase-server) |
| [Supply chain research loop](loops/supply-chain-research-loop/LOOP.md) | Dated research priorities, rechecked monthly. | monthly theme rescan | [page](https://gethabit.dev/skills/muxuuu/serenity-skill) |
| [Surface audit loop](loops/surface-audit-loop/LOOP.md) | Surface matches the model below. | model or flow changes | [page](https://gethabit.dev/skills/jamiemill/layers-surface) |
| [Svelte autofixer loop](loops/svelte-autofixer-loop/LOOP.md) | Ship Svelte components the autofixer accepts. | Svelte files changed | [page](https://gethabit.dev/skills/sveltejs/svelte-code-writer) |
| [Swift 6 migration loop](loops/swift6-migration-loop/LOOP.md) | One diagnostic category cleared per run. | every weeknight | [page](https://gethabit.dev/skills/avdlee/swift-concurrency) |
| [SwiftData review loop](loops/swiftdata-review-loop/LOOP.md) | SwiftData bugs caught before merge. | Swift pull request opened | [page](https://gethabit.dev/skills/twostraws/swiftdata-pro) |
| [SwiftUI review loop](loops/swiftui-review-loop/LOOP.md) | SwiftUI changes pass the checklist. | PR changes Swift files | [page](https://gethabit.dev/skills/avdlee/swiftui-expert-skill) |
| [Root cause debugging loop](loops/systematic-debugging-loop/LOOP.md) | Every bug fixed at its source. | test or build fails | [page](https://gethabit.dev/skills/obra/systematic-debugging) |
| [Tailwind docs refresh loop](loops/tailwind-docs-refresh-loop/LOOP.md) | Tailwind v4 docs never go stale. | every Monday morning | [page](https://gethabit.dev/skills/lombiq/tailwind-4-docs) |
| [Task breakdown loop](loops/task-breakdown-loop/LOOP.md) | Turn each spec into small tasks. | spec gets approved | [page](https://gethabit.dev/skills/addyosmani/planning-and-task-breakdown) |
| [Tauri v2 health loop](loops/tauri-v2-health-loop/LOOP.md) | Tauri commands and permissions stay wired. | src-tauri changed | [page](https://gethabit.dev/skills/nodnarbnitram/tauri-v2) |
| [Tavily news watch loop](loops/tavily-news-watch-loop/LOOP.md) | Daily news on your topics. | daily news search | [page](https://gethabit.dev/skills/tavily-ai/tavily-search) |
| [Tavily weekly research loop](loops/tavily-weekly-research-loop/LOOP.md) | A fresh cited report every week. | Mondays at 07:00 | [page](https://gethabit.dev/skills/tavily-ai/tavily-research) |
| [Tech spec loop](loops/tech-spec-loop/LOOP.md) | Plans grounded in the real code. | product spec approved | [page](https://gethabit.dev/skills/warpdotdev/write-tech-spec) |
| [Technical doc review loop](loops/technical-doc-review-loop/LOOP.md) | Docs stay sourced, current and plain. | PR changes a document | [page](https://gethabit.dev/skills/riekelt/technical-writing) |
| [Template builder audit loop](loops/template-builder-audit-loop/LOOP.md) | Template editors save valid Sent payloads. | PR changes template builder | [page](https://gethabit.dev/skills/sentdm/template-builder-ui) |
| [Terse commit message loop](loops/terse-commit-message-loop/LOOP.md) | Every commit message short and exact. | commit message requested | [page](https://gethabit.dev/skills/juliusbrussee/caveman-commit) |
| [Test anti-pattern audit loop](loops/test-anti-pattern-audit-loop/LOOP.md) | Tests that prove nothing get caught. | test files change | [page](https://gethabit.dev/skills/dotnet/test-anti-patterns) |
| [Red green refactor loop](loops/test-driven-development-loop/LOOP.md) | Every change starts with a test. | feature or bugfix task | [page](https://gethabit.dev/skills/obra/test-driven-development) |
| [Three.js game profile loop](loops/threejs-game-profile-loop/LOOP.md) | Root causes fixed, bottlenecks measured. | bug or slowdown reported | [page](https://gethabit.dev/skills/majidmanzarpour/threejs-debug-profiler) |
| [Three.js playable slice loop](loops/threejs-playable-slice-loop/LOOP.md) | A game loop you can play. | you build a mechanic | [page](https://gethabit.dev/skills/majidmanzarpour/threejs-gameplay-systems) |
| [Tigris native SDK check loop](loops/tigris-native-sdk-check-loop/LOOP.md) | Code uses native Tigris SDKs. | PR changes storage dependencies | [page](https://gethabit.dev/skills/tigrisdata/tigris-sdk-guide) |
| [Tigris security audit loop](loops/tigris-security-audit-loop/LOOP.md) | Storage keys and CORS stay tight. | monthly storage security audit | [page](https://gethabit.dev/skills/tigrisdata/tigris-security-access-control) |
| [TikTok trend watch loop](loops/tiktok-trend-watch-loop/LOOP.md) | Track TikTok trends for your keywords. | daily TikTok trend watch | [page](https://gethabit.dev/skills/fetcher-sh/tiktok-api) |
| [Token diet loop](loops/token-diet-loop/LOOP.md) | Every session short and cheap. | every new session | [page](https://gethabit.dev/skills/juliusbrussee/caveman) |
| [Topic research report loop](loops/topic-research-report-loop/LOOP.md) | Tracked topics get fresh research reports. | weekly topic research | [page](https://gethabit.dev/skills/actionbook/active-research) |
| [Turso compat triage loop](loops/turso-compat-triage-loop/LOOP.md) | Each mismatch traced to its layer. | SQLite mismatch reported | [page](https://gethabit.dev/skills/tursodatabase/debugging) |
| [X topic watch loop](loops/twitter-topic-watch-loop/LOOP.md) | Daily digest of your X topics. | daily topic search | [page](https://gethabit.dev/skills/resciencelab/twitter) |
| [Typefully queue fill loop](loops/typefully-queue-fill-loop/LOOP.md) | Next week's social queue drafted. | weekly queue fill | [page](https://gethabit.dev/skills/typefully/typefully) |
| [Typography review loop](loops/typography-review-loop/LOOP.md) | Text renders right on every PR. | PR touches styles | [page](https://gethabit.dev/skills/jakubkrehel/better-typography) |
| [Typst build check loop](loops/typst-build-check-loop/LOOP.md) | Typst documents always compile cleanly. | .typ file changed | [page](https://gethabit.dev/skills/lucifer1004/typst) |
| [UI animation review loop](loops/ui-animation-review-loop/LOOP.md) | Smooth motion in every PR. | PR touches animation code | [page](https://gethabit.dev/skills/mblode/ui-animation) |
| [UI motion review loop](loops/ui-motion-review-loop/LOOP.md) | Animations reviewed on every UI change. | PR touches UI code | [page](https://gethabit.dev/skills/emilkowalski/emil-design-eng) |
| [UI polish review loop](loops/ui-polish-review-loop/LOOP.md) | UI details stay exact and consistent. | PR touches UI code | [page](https://gethabit.dev/skills/jakubkrehel/better-ui) |
| [UI taste loop](loops/ui-taste-loop/LOOP.md) | Keep every UI change on taste. | PR changes UI files | [page](https://gethabit.dev/loops/ui-taste-loop) |
| [UI4 reskin loop](loops/ui4-reskin-loop/LOOP.md) | One component reskinned to match Figma. | next component on board | [page](https://gethabit.dev/skills/payloadcms/ui4) |
| [UI test fix loop](loops/ui4-test-fix-loop/LOOP.md) | E2E tests follow UI changes. | UI change ready | [page](https://gethabit.dev/skills/payloadcms/ui4-convert-tests) |
| [UI4 token review loop](loops/ui4-token-review-loop/LOOP.md) | CSS uses tokens, not hardcoded values. | CSS files changed | [page](https://gethabit.dev/skills/payloadcms/ui4-review) |
| [Uniwind style rules loop](loops/uniwind-style-rules-loop/LOOP.md) | React Native styles follow Uniwind rules. | component files change | [page](https://gethabit.dev/skills/uni-stack/uniwind) |
| [Unslop docs loop](loops/unslop-docs-loop/LOOP.md) | Strip AI tells from new docs. | docs text changes | [page](https://gethabit.dev/skills/backnotprop/unslop) |
| [User feedback synthesis loop](loops/user-feedback-synthesis-loop/LOOP.md) | Turn feedback into clear decisions. | weekly feedback review | [page](https://gethabit.dev/skills/refoundai/analyzing-user-feedback) |
| [Skill validation loop](loops/validate-skills-loop/LOOP.md) | Every skill passes the spec. | PR touches skills folder | [page](https://gethabit.dev/skills/callstackincubator/validate-skills) |
| [VHS demo evidence loop](loops/vhs-demo-evidence-loop/LOOP.md) | Before and after GIFs reviewers trust. | CLI output changes | [page](https://gethabit.dev/skills/cli/vhs-demo) |
| [Vibe security audit loop](loops/vibe-security-audit-loop/LOOP.md) | Common AI-coded security holes caught. | code changes | [page](https://gethabit.dev/skills/raroque/vibe-security) |
| [Video prompt loop](loops/video-prompt-loop/LOOP.md) | Video prompts that direct the shot. | new clip brief | [page](https://gethabit.dev/skills/replicate/prompt-videos) |
| [Video watch digest loop](loops/video-watch-digest-loop/LOOP.md) | Saved videos turned into timestamped notes. | video added to list | [page](https://gethabit.dev/skills/bradautomates/watch) |
| [Vite bundle loop](loops/vite-bundle-loop/LOOP.md) | Your Vite bundle stays lean. | PR opened or updated | [page](https://gethabit.dev/skills/asyrafhussin/react-vite-best-practices) |
| [Vue warning triage loop](loops/vue-warning-triage-loop/LOOP.md) | Vue warnings get fixed, not ignored. | Vue warning in logs | [page](https://gethabit.dev/skills/vuejs-ai/vue-debug-guides) |
| [W&B project digest loop](loops/wandb-project-digest-loop/LOOP.md) | Daily digest of runs and traces. | every morning | [page](https://gethabit.dev/skills/wandb/wandb-primary) |
| [Web extract loop](loops/web-extract-loop/LOOP.md) | Fresh structured data from websites. | daily extract run | [page](https://gethabit.dev/skills/actionbook/extract) |
| [Web typography check loop](loops/web-typography-check-loop/LOOP.md) | Type stays readable on every release. | CSS or fonts change | [page](https://gethabit.dev/skills/wondelai/web-typography) |
| [WeChat draft loop](loops/wechat-draft-loop/LOOP.md) | Finished posts land as drafts. | article marked ready | [page](https://gethabit.dev/skills/jimliu/baoyu-post-to-wechat) |
| [WeCom meeting notes loop](loops/wecom-meeting-notes-loop/LOOP.md) | Every meeting gets its notes. | Workdays at 18:00 | [page](https://gethabit.dev/skills/wecomteam/wecomcli-meeting) |
| [WeCom todo digest loop](loops/wecom-todo-digest-loop/LOOP.md) | Open todos reviewed every morning. | workday morning digest | [page](https://gethabit.dev/skills/wecomteam/wecomcli-todo) |
| [WhatsApp template lint loop](loops/whatsapp-template-lint-loop/LOOP.md) | WhatsApp templates pass review first time. | template needed or rejected | [page](https://gethabit.dev/skills/sentdm/waba-template-author) |
| [Wiki health audit loop](loops/wiki-health-audit-loop/LOOP.md) | Your wiki stays linked and current. | weekly health check | [page](https://gethabit.dev/skills/ar9av/wiki-lint) |
| [Wiki ingest distill loop](loops/wiki-ingest-distill-loop/LOOP.md) | New sources distilled into wiki pages. | new source to ingest | [page](https://gethabit.dev/skills/ar9av/wiki-ingest) |
| [Wiki query answer loop](loops/wiki-query-answer-loop/LOOP.md) | Cited answers from your own wiki. | you ask a question | [page](https://gethabit.dev/skills/ar9av/wiki-query) |
| [Wiki status delta loop](loops/wiki-status-delta-loop/LOOP.md) | Always know what the wiki needs. | weekly status check | [page](https://gethabit.dev/skills/ar9av/wiki-status) |
| [Workflow security review loop](loops/workflow-security-review-loop/LOOP.md) | Catch risky CI workflow changes. | workflow file changed | [page](https://gethabit.dev/skills/superagent-ai/ci-cd-security) |
| [Wrangler config check loop](loops/wrangler-config-check-loop/LOOP.md) | Config changes checked before deploy. | Wrangler config changed | [page](https://gethabit.dev/skills/cloudflare/wrangler) |
| [Implementation plan loop](loops/writing-plans-loop/LOOP.md) | Every spec becomes a plan. | new spec committed | [page](https://gethabit.dev/skills/obra/writing-plans) |
| [X search watch loop](loops/x-search-watch-loop/LOOP.md) | New posts on your topics, daily. | daily topic search | [page](https://gethabit.dev/skills/fetcher-sh/twitter-api) |
| [Xcode build audit loop](loops/xcode-build-audit-loop/LOOP.md) | A ranked, approved build speed-up plan. | You request a build audit | [page](https://gethabit.dev/skills/avdlee/xcode-build-orchestrator) |
| [Xcode fix benchmark loop](loops/xcode-fix-benchmark-loop/LOOP.md) | Approved build fixes proven by benchmark. | plan approved | [page](https://gethabit.dev/skills/avdlee/xcode-build-fixer) |
| [Xcode project audit loop](loops/xcode-project-audit-loop/LOOP.md) | Project-level build waste found and ranked. | you ask for project audit | [page](https://gethabit.dev/skills/avdlee/xcode-project-analyzer) |
| [Xiaohongshu content plan loop](loops/xhs-content-plan-loop/LOOP.md) | Notes planned and posted with approval. | weekly content planning | [page](https://gethabit.dev/skills/autoclaw-cc/xiaohongshu) |
| [Japanese polish loop](loops/yomiyasu-loop/LOOP.md) | Natural Japanese in every draft. | new Japanese draft added | [page](https://gethabit.dev/skills/nanaism/yomiyasu) |
| [YouTube channel watch loop](loops/youtube-channel-watch-loop/LOOP.md) | A daily record of channel uploads. | daily channel check | [page](https://gethabit.dev/skills/fetcher-sh/youtube-api) |
| [YouTube channel watch loop](loops/zeropointrepo-youtube-channel-watch-loop/LOOP.md) | New videos from your channels, summarized. | daily channel check | [page](https://gethabit.dev/skills/zeropointrepo/youtube-full) |
| [Ziniao access rule review loop](loops/ziniao-access-rule-review-loop/LOOP.md) | Access rules reviewed every week. | weekly access rule review | [page](https://gethabit.dev/skills/ziniao-open/ziniao-access-policy) |
| [Ziniao store access audit loop](loops/ziniao-store-auth-audit-loop/LOOP.md) | Store access and tags stay clean. | weekly store access audit | [page](https://gethabit.dev/skills/ziniao-open/ziniao-account) |
| [Knowledge Planet patrol loop](loops/zsxq-daily-patrol-loop/LOOP.md) | What needs your reply, daily. | daily group patrol | [page](https://gethabit.dev/skills/unnoo/zsxq) |

MIT licence for the habit files. Each skill keeps its own licence.
