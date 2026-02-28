# Project Vocabulary

<!-- Terms, jargon, acronyms specific to this project -->
<!-- Updated by Spec Writer agent when new terms are introduced -->

<!-- Example:
| Term | Meaning | First seen |
|------|---------|------------|
| workspace | A processing session for one anonymized dataset | Session 2026-02-27 |
| stent-graft | Medical device: metal mesh (stent) + fabric tube (graft) | Session 2026-02-27 |
-->

| Term | Meaning | First seen |
|------|---------|------------|
| SDD | Spec-Driven Development — formal specs before code | 2026-02-27 |
| TDD | Test-Driven Development — write tests before implementation | 2026-02-27 |
| REQ | Requirement — atomic spec unit, 3-7 acceptance tests each | 2026-02-27 |
| CR | Change Request — modification to existing REQ | 2026-02-27 |
| PLAN | Implementation plan created by Architect for a REQ | 2026-02-27 |
| Agent Teams | Native Claude Code feature for parallel agent coordination | 2026-02-27 |
| wshobson/agents | Community project (29.5k stars) — plugins, 3-tier model strategy | 2026-02-27 |
| claude-flow | Ruflo — orchestrator (15.3k stars), context archival | 2026-02-27 |
| OpenClaw | Messaging AI platform (236k stars) — gateway, hooks, cron patterns | 2026-02-27 |
| MCP | Model Context Protocol — agent↔tools communication | 2026-02-27 |
| ACP | Agent Context Protocol — agent↔agent communication (future Phase 3+) | 2026-02-27 |
| Copier | Python project templating with 3-way merge updates | 2026-02-27 |
| 3-tier model | Opus ($15/1M) → Sonnet ($3/1M) → Haiku ($0.80/1M) routing | 2026-02-27 |
| progressive disclosure | 3-tier prompt loading: metadata → instructions → resources | 2026-02-27 |
| Conductor | wshobson pattern: persistent state, semantic revert, track/phase/task | 2026-02-27 |
| gateway pattern | OpenClaw: single entry point routing messages to agents | 2026-02-27 |
| lifecycle hooks | session_start/end, before/after_tool_call, agent:bootstrap | 2026-02-27 |
| SPEC_INDEX | Registry file tracking all REQs and their statuses | 2026-02-27 |
| PRIORITY.md | Scoring algorithm for requirement selection | 2026-02-27 |
| NanoClaw | Lightweight OpenClaw on Agent SDK, containerized | 2026-02-27 |
