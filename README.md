# Amicus Releases

**Desktop AI Agent — 대화만으로 컴퓨터의 모든 작업을 수행합니다.**

최신 버전은 [Releases](https://github.com/Altair-Hyun/amicus-releases/releases)에서 내려받으세요.

| Platform | File |
|----------|------|
| **macOS** (Universal) | `Amicus-<version>-universal.dmg` |
| **Windows** (x64) | `Amicus Setup <version>.exe` |

---

## 시작하기 (사전 작업)

### macOS — 서명 안 된 앱 실행
Amicus는 코드 서명이 없어 첫 실행 시 "알 수 없는 개발자" 경고가 뜹니다. 설치 후 아래를 실행하세요:

```sh
xattr -cr /Applications/Amicus.app
```

### Python 3.11 이상 (필수)
Amicus는 Python을 번들하지 않습니다. 백엔드가 Python 사이드카로 동작하므로, Python이 없으면 앱은 켜지되 자동화·세션·에이전트 루프가 동작하지 않습니다.

| OS | 설치 |
|----|------|
| **Windows** | `winget install Python.Python.3.12` (또는 [python.org](https://www.python.org/downloads/windows/)에서 설치 시 **"Add python.exe to PATH"** 체크) |
| **macOS** | `brew install python@3.12` |

> 3.11 미만은 지원하지 않습니다. Python 패키지는 첫 실행 시 `~/.amicus/venv`에 **자동 설치**됩니다(사용자 조치 불필요).

---

## 패치노트

<!-- AUTO-APPEND: 태그 push마다 이 줄 바로 아래에 최신 릴리스 섹션이 추가됩니다. -->

### v1.9

**Theme:** Reliability hardening of the AI agent loop, a rebuilt "smart" Watcher, MCP support, a real login/data-integrity gate, and the move to a shared-store architecture — the longest-running and largest line in the project (June 8 – August 13, ~789 commits).

`v1.9.0 … v1.9.4-smoke.6`

- **Agent-loop "never-STOP" reliability rework**: root-caused and fixed a class of silent run terminations — `flow_plan` treated as a fake terminal answer, Bedrock dropping a stream event on soft-idle (corrupted tool-call JSON), collector stragglers misclassified as retryable timeouts causing 50-minute stalls, malformed tool-calls, and repeated-failure guards silently swallowing partial results. Later replaced the whole pre-loop intent/sizing/strategy LLM round-trip with a fixed safety cap, and removed `flow_plan` from the model-facing tool surface entirely in favor of runtime-owned fan-out.
- **Watcher rebuilt into a shape-aware, provider-neutral monitor**: URL/JSON probe that infers structure automatically (arrays, identity fields, nested paths), an interactive shape-tree picker UI, and/or condition groups, per-item dedup via stable identity paths (including nested arrays, e.g. per-Jira-comment alerts), and template-free `{watcher_text}` auto-formatting of any payload.
- **MCP (Model Context Protocol) client support** added end-to-end: stdio + HTTP transports with bearer auth, per-server tool aggregation, config UI, and a `{server}` marker to force a specific MCP tool — after an earlier, fully custom "Known Work" vector-knowledge-base feature (Postgres/pgvector, Trino, Qdrant, embedded SQLite backends, built over ~3 days) was scrapped and removed in favor of it.
- **Workflow engine rewritten** around a step-handler registry (shell/notify/slack/email/condition/wait/parallel/`ai_prompt`/`if`/`http_request`), full per-step input/output/error capture in run history, drag-to-reorder steps with forward-reference warnings, and workflow-owned cron schedules.
- **Login/data-integrity gate landed**: production Cognito login gate (group-based access, silent refresh, fail-closed) shipped after earlier "Signal" login-gate scaffolding, alongside a store read/write split (Electron reads a shared SQLite store, backend is sole writer; `.amicus-v2` → `.amicus` folder consolidation) fixing run-history that silently vanished across restarts, plus an async store-prepare rewrite to kill a Windows "Not Responding" boot hang caused by main-thread blocking spawns.
- **Sidecar/backend platform work**: `apps/desktop` folded into `src/`, sidecar lifecycle hardened against orphaned/zombie processes with bounded respawn, chat-run store moved to SQLite with TTL pruning and a concurrency semaphore, and the backend Python bootstrap made fully async with a splash-screen progress UI and a diagnostics/venv-repair panel.
- **Terminal & approval UX overhaul**: per-tool approval gate rebuild ("approve all this turn"), a redesigned terminal (separate xterm for tool output vs. interactive shell, ConPTY/Windows scroll fixes), window chrome simplified (start maximized, app menu removed), and an `ask_user` virtual tool that can pause a run for confirmation or masked secret input (e.g. sudo password) without leaking it into the transcript.
- **Provider/integration breadth**: Slack Watcher rewritten on Socket Mode (backend-driven, content-aware dedup, autonomous root-cause-analysis notifications), a backend Notifications domain with per-alert analysis threads, live AI model listing + provider budget/prompt-cache policy across Anthropic/OpenAI/Bedrock/Gemini/Codex/Ollama, and outbound HTTP routed through Electron's network stack so it respects the corporate VDI proxy.
- **Chat session auto-titling**: provider-neutral one-shot summary generates a real session title instead of the first message, updating the sidebar live.
- Numerous smaller fixes: CSV/report path cleanups, GitLab/GitHub token-drop-on-save fix, Bedrock `ListInferenceProfiles` pagination, GFM task-list checkbox rendering, and a release-CI fix so `-smoke.` prerelease tags stop publishing as `latest`.

### v1.8

**Theme:** Execution-contract completion tracking, `http_request` maturity, and a large dead-code purge of provider-specific integration methods in favor of the generic HTTP tool.

`v1.8.0 … v1.8.2-mock.1`

- Added an **execution-contract model** so the agent loop keeps running until there's real evidence of completion, instead of stopping early on a plan-only turn (superseding an earlier "API fanout reconciliation" experiment that was implemented, found to override multi-part plans with a single API result, and promptly removed).
- Enforced **multi-job completion** for bundled/compound requests so a multi-part ask isn't silently collapsed to one job.
- Matured `http_request` into a first-class collection tool: provider-neutral query serialization, idempotent retry with backoff/`Retry-After`, and NDJSON spooling of large paginated results to disk.
- **Large cleanup**: removed dead-code integration methods across Jira/Confluence/GitHub/GitLab/Slack/Gmail now superseded by `http_request`, deleted the standalone `facts_aggregate` tool (data_inspect is the sole data SSOT), and dropped unused dependencies (handlebars, etc.).
- Added **live AI model listing** (Anthropic/OpenAI/Bedrock) with hardcoded fallback, and bundled Google OAuth Desktop credentials so "Login with Google" works out of the box.
- Perf pass: async/parallel system-info probes with a persistent cache and startup prewarm, cutting first-message latency.

### v1.7

**Theme:** Chat history becomes durable and backend-owned, and the collector/execution stack gets a major provider-neutral architecture pass (VDI hardening line).

`v1.7.0 … v1.7.2-vdi-smoke.48`

- Built a proper **chat-history persistence layer** (SQLite tables + indexes, resumable runs, cursor-based capture) and rewired the sidebar/session list to read from it instead of legacy in-memory state.
- **`python_execute` became the canonical execution/report path**: classifier + args/cwd/timeout-aware executor with streaming and audit telemetry, culminating in auto-registering `.html` stdout as a report artifact — this is also where the older `report_generate` / `report_pipeline` / `direct_html_report` template machinery was superseded.
- **Bulk execution model rewrite** ("flow_plan" naming, PR-α/β series): moved environment/PATH/shell-family resolution out of TypeScript entirely and into the Python side (`amicus_run.py`) for parity between local and collector execution.
- **`data_inspect` established as the single source of truth** for structured file/data inspection (overview-by-default, YAML/TOML/XML structural counts, provider-neutral prompt gating), retiring parallel ad hoc paths.
- Collector hardening for VDI environments: kept parallel runs alive/resumable across flaky connections, derived batch parallelism from live probe timing instead of static guesses.

### v1.6

**Theme:** The single largest line (626 commits, April 14 – May 20) — a provider-neutral rebuild of the collection/adapter stack, a huge expansion of integration tools, the birth of the Python backend sidecar, and the start of chat ownership moving server-side.

`v1.6.0 … v1.6.128`

- **Windows compatibility hardening**: fixed native `.exe` hangs under Git Bash (routed through `cmd.exe`/PTY), AWS SSO token cache sync, process-tree kill via `taskkill /T`, and a large body of shell/PATH/CLI edge cases.
- **Provider-neutral adapter architecture**: introduced a `ProviderAdapter` protocol with a Python bridge, adapter versioning/audit trail, and a "shared-layer bias guard" CI check to keep vendor-specific logic out of shared code — plus production adapters for Kubernetes (in-cluster EKS bootstrap) and AWS (boto3).
- **Integration surface roughly tripled**: ~40 new tools added across Jira (11), Confluence (7), GitHub (9), GitLab (5), Slack (6), and Notion (3), with pagination support and read-only same-turn parallel dispatch.
- **Report generation matured**: HTML reports gained XLSX (multi-sheet) export, auto-inlined CSS for email compatibility, Handlebars-style templating, and a `batch_plan` tool that publishes upfront K/P/T (target/parallelism/timeout) sizing to the user.
- **The Python backend was born** (tagged mid-line as `v1.0.0-renew`, "Architect V2 runtime gateway skeleton") — a FastAPI-style `apps/backend` service with its own contracts, adapters, and API surface, separate from the Electron main process.
- **Chat ownership began moving to the backend**: the agent loop, streaming, progress reporting, and report generation were progressively re-owned by the Python sidecar rather than the Electron/TS layer ("backend agent loop SoT"), including a sidecar auto-bootstrap with its own managed Python 3.14 venv.
- Closed out with structured-progress UI rework (per-child result rows, adaptive `maxLoopUse`), a chat `/state` payload-bloat fix series, and the first version of `python_execute` as an install-hook–integrated runner.

### v1.5

**Theme:** Terminal/session-state reliability plus the first "embedded services" performance/infrastructure pass.

`v1.5.0 … v1.5.9`

- Fixed a cluster of terminal/session bugs: chat history surviving session re-clicks, terminal history surviving tab switches (singleton xterm + `React.memo`), a Windows `shell_execute` hang (exit-event + pipe-destroy fix), and AWS SSO token hangs.
- Added an `excel_create` tool (multi-sheet, styled headers via ExcelJS) and a custom-prompts tab.
- Enforced parallel shell execution for bulk operations and banned "announcement-only" AI responses that don't follow through with action.
- **Embedded services infrastructure** rolled out in phases: indexes/cache/circuit-breaker/persistent queue (Phase 1), croner/pino/bottleneck/p-queue (Phase 2), vectra/MCP-health/Handlebars (Phase 3) — plus migrating ~118 `console.log` calls to a structured logger.
- Closed the line by resolving all outstanding test failures (173/173 passing).

### v1.4

**Theme:** A short, single-feature bridge release.

`v1.4.0`

- Added an `excel_create` tool via ExcelJS.
- Added a custom-prompts tab (renamed the env-vars tab to Korean "보안").

### v1.3

**Theme:** Windows shell-execution edge cases and CLI non-interactivity.

`v1.3.0 … v1.3.4`

- Fixed native `.exe` execution on Windows Git Bash (winpty wrapper, then reverted `cmd.exe` routing after discovering `spawn` uses a pipe, not a PTY, avoiding a console deadlock).
- Forced non-interactive environment variables universally across CLI tools (not just AWS) to stop pager/prompt hangs.
- Banned useless `echo`/`sleep` commands and required the AI to run login commands itself rather than asking the user to.
- Always surface executed commands in the terminal for transparency.

### v1.2

**Theme:** Windows environment-variable and shell-execution correctness.

`v1.2.0 … v1.2.9`

- Read the full Windows system PATH from the registry for child processes, and switched to inheriting the full `process.env` instead of an allowlist filter.
- Used login shells (`--login`) and loaded the user's PowerShell profile with `ExecutionPolicy Bypass` for consistent tool availability.
- Routed Windows native `.exe` execution through `cmd.exe` to avoid Git Bash PTY hangs.
- Fixed CSV export Excel/UTF-8 compatibility and prevented Microsoft Store Python stub hangs with a timeout.

### v1.1

**Theme:** Shell-detection and execution-policy consistency between the terminal and AI tool calls.

`v1.1.0 … v1.1.9`

- Unified shell detection so `shell_execute` matches the interactive PTY (Git Bash preferred on Windows, PowerShell as an explicit fallback only).
- Fixed abort handling dropping the `tool_result`, and improved chat output readability.
- Added a user-configurable execution policy with a blocked-reason display, and polished the "AI running" banner (shimmer/bouncing-dots).

### v1.0

**Theme:** The 1.0 milestone — accessibility, i18n, resilience patterns, and safer environment-variable handling.

`v1.0.0 … v1.0.9`

- Added Circuit Breaker resilience for external API calls, i18n (ko/en) via i18next, message search (Cmd+F), and Google Sheets integration.
- Improved accessibility (ARIA labels, keyboard nav, contrast) and added HTML/CSV chat export.
- Switched environment-variable handling from an allowlist to a user-configurable **blocklist**, passing the full user environment through to child processes by default (fixing a long tail of "missing PATH/env" issues) while letting users still redact secrets.
- Refactored IPC handlers into focused modules and extracted shared workflow/registry helper functions as the codebase grew.
- Applied "approve" execution mode consistently to all tools, and made abort actually stop the tool loop.

### v0.9

**Theme:** A dedicated security-hardening release plus template/UI polish.

`v0.9.0 … v0.9.8`

- **Security release (v0.8.0 relabeled here)**: fixed 6 critical vulnerabilities and memory leaks, closed an email-header-injection hole and a markdown XSS vector, and added IPC type-safe argument validation.
- Implemented 24 medium-priority backend/frontend improvements identified in the security review.
- Fixed template duplication/dedup bugs on app restart (scoped dedup to default template names only).
- Raised `maxTokens` from 8192 → 16384 and fixed chat-history pairing of `tool_use`/`tool_result` blocks around approve-mode timing.
- UI polish: app-wide animations, environment-variables tab, Windows loading-dots animation and text wrapping.

### v0.8

**Theme:** Completing the HTML report-template catalog.

`v0.7.3 … v0.8.4`

- Completed the full report template catalog (13 templates, each with HTML + Markdown + prompt + data-source metadata).
- Shipped "security+perf" fixes across policy enforcement, environment variables, CI, and compression.
- Rebalanced the default window/panel layout (1200×800 → 1400×900; chat panel 35% → 50%) for a 1:1 center:chat ratio.

### v0.7

**Theme:** Template system consolidation and a first pass at deep multi-step investigation.

`v0.6.2 … v0.7.3`

- Unified template naming and added message-variant support; auto-migrated deprecated Korean template names on startup.
- Added 4 new HTML preview templates (incident-k8s, daily-status, security-alert, slack-digest).
- Introduced a "deep analysis chain" — multi-layer investigation prompting usable across all contexts.

### v0.6

**Theme:** Rapid report-template expansion.

`v0.5.0 … v0.6.2`

- Added a monthly ops report template (with a v2 animated/enhanced revision) and 5 more templates (incident, deploy, cost, security, SLA).
- Added CSV download to all report templates and a copy-paste-ready "prompt guide" for generating reports.
- Added an in-app template usage-guide tab.

### v0.5

**Theme:** File management and workflow flexibility.

`v0.4.2 … v0.5.0`

- Added a file-explorer with full CRUD (create/rename/delete files and folders).
- Added per-service "preferred accounts" for workflows and full Notion integration (DB query/list/create/delete/update row).
- Added parallel sub-step execution within workflows.

### v0.4

**Theme:** A brief cleanup/polish stop between v0.3 and v0.5.

`v0.4.0 … v0.4.2`

- Added dynamic `maxTokens` sizing and an "Open Folder" button after `file_write`.
- Made chat file paths clickable (opens in Finder/Explorer).
- Resolved all TypeScript lint errors and removed the Slack Bot Token path in favor of the linked user token.

### v0.3

**Theme:** Ticketing/DevOps integrations (Jira, Confluence, GitHub, GitLab) and report templating groundwork.

`v0.2.9 … v0.3.9`

- Added GitHub and GitLab integrations (both cloud and on-premise), and Jira/Confluence Cloud vs. Server/Data-Center API compatibility with PAT (Bearer) auth.
- Introduced report presets and HTML templates (e.g. a Korean-language "Daily Jira Status" template) plus a template catalog/gallery with AI auto-variable extraction from uploaded templates.
- Hardened `file_write` (path aliasing, `~` expansion, rejecting empty-content writes) and fixed `tool_call_delta` argument assembly for streamed tool calls.
- Raised `maxTokens` from 4096 → 16384 with truncation detection on Bedrock/Claude.

### v0.2

**Theme:** The automation model (Watcher/Cron/Workflow) got its first real redesign, plus cross-platform (Windows) terminal work.

`v0.1.0 … v0.2.9`

- Redesigned automation around a `WorkflowQueue` (concurrency limits, overflow control): Cron now triggers workflows instead of running the AI directly, and Watcher notifies workflows via `workflowIds` instead of ad hoc actions, with legacy configs auto-migrated.
- Added Windows terminal support: auto-detected Git Bash/Cygwin/WSL, synced terminal cwd with the file explorer, and fixed AWS credential parsing and path conversion (`/cygdrive/c/` → `C:\`) along the way.
- Added connected-account management (click to disconnect) and separated Jira/Confluence as independent connections.
- Set up CI to auto-upload releases to a separate `amicus-releases` repo, and hardened login-token persistence across app restarts.

### v0.1

**Theme:** The original scaffold — from an empty Electron shell to a working AI desktop agent with terminal, browser automation, MCP tools, and a first automation layer, in about a week.

`v0.1.0` (first commit 2026-03-24 → first tag 2026-03-31)

- Bootstrapped the Electron app: IPC registry, System/Executor/AI services, an approval-gated execution policy engine, and Claude/ChatGPT provider support (subscription web login + API key dual auth).
- Built the core UI: Tokyo-Night-themed layout with a Chat Panel, an xterm.js Terminal Panel, and a complete tool-calling loop (`shell_execute`, `file_read`, `file_write`).
- Added desktop agent tools — AppleScript, screenshot, clipboard, notifications — plus Playwright browser automation and an MCP client (desktop-commander, filesystem, Playwright servers).
- Delivered an interactive PTY terminal (real zsh/bash via node-pty) with AI commands routed through the same PTY for identical output, after multiple iterations to fix garbled/marker-polluted output.
- Introduced Memory (SQLite + FTS search), session persistence, and the first automation primitives: Cron scheduler, Watcher (event monitor), and Workflow (pipeline), plus a webhook receiver for Slack/Grafana/PagerDuty.
- Added Bedrock as a third AI provider, SMTP email, system tray, and a GitHub Actions CI/build pipeline (macOS + Windows).
