# Decisions Log

<!-- Append-only. Each decision includes rationale and date. -->
<!-- Format: ### D-NNN: <decision title> -->

### D-001: Build SDD layer, not orchestrator
- **Date**: 2026-02-27
- **Decision**: Our framework = methodology + templates + rules. NOT another agent orchestrator.
- **Rationale**: Market saturated with orchestrators (wshobson 29.5k stars, claude-flow 15.3k, Agent Teams native). Nobody owns SDD + TDD methodology end-to-end.
- **Alternatives considered**: CrewAI (too abstract), custom Agent SDK (premature), full orchestrator (can't compete)

### D-002: Agent Teams as execution engine
- **Date**: 2026-02-27
- **Decision**: Use Claude Code Agent Teams for parallel agent coordination.
- **Rationale**: Native Anthropic feature, no custom code needed.
- **Limitations**: No session resumption, experimental, one team per session.
- **Mitigation**: Our memory system fills the persistence gap.

### D-003: wshobson/agents for capabilities
- **Date**: 2026-02-27
- **Decision**: Use wshobson/agents plugins for TDD, code review, debugging capabilities.
- **Rationale**: 29.5k stars, mature, install-what-you-need. 3-tier model routing saves ~49% tokens.

### D-004: Copier for project templating
- **Date**: 2026-02-27
- **Decision**: Copier instead of Cookiecutter.
- **Rationale**: Copier supports `copier update` — 3-way merge to pull template improvements into existing projects.

### D-005: Memory as markdown first
- **Date**: 2026-02-27
- **Decision**: Start with markdown files in agents/*/memory/.
- **Rationale**: Simple, git-tracked, works now. Upgrade to SQLite + semantic search when hitting context limits.

### D-006: OpenClaw patterns, not platform
- **Date**: 2026-02-27
- **Decision**: Take architecture patterns from OpenClaw (gateway routing, lifecycle hooks, cron scheduler, selective skill injection). Don't use OpenClaw itself.
- **Rationale**: OpenClaw is a messaging assistant platform. We need its architectural ideas for our dev workflow.

### D-007: MCP for tools, ACP for agents
- **Date**: 2026-02-27
- **Decision**: MCP now (agent↔tools), evaluate ACP for Phase 3+ (agent↔agent).
- **Rationale**: Complementary protocols. File-based handoff works for Phase 0-1.
