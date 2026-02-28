# Session History

<!-- Append-only log. Each session adds a summary at the end. -->
<!-- This helps the agent recall what was discussed previously. -->

<!-- Example:
## Session 2026-02-27 — Initial project setup
- Discussed: project scope, target users, tech stack
- Created: REQ-001, REQ-002, REQ-003
- Decided: JWT auth, PostgreSQL, REST API
- Open: payment provider choice (Q-003)
-->

## Session 2026-02-27 — Project bootstrap & architecture research
- **Discussed**: full project architecture, competitive landscape, what to build vs reuse
- **Created**: ARCHITECTURE.md, TODO.md (detailed), CLAUDE.md (project config)
- **Researched**: wshobson/agents, claude-flow, OpenClaw, CrewAI, Kiro, Agent Teams, ACP
- **Decided**:
  - D-001: Build SDD methodology layer, NOT another orchestrator
  - D-002: Agent Teams as execution engine
  - D-003: wshobson/agents for capabilities (plugins, 3-tier models)
  - D-004: Copier for project templating (not Cookiecutter)
  - D-005: Memory as markdown first, SQLite later
  - D-006: OpenClaw patterns (gateway, hooks, cron), not platform
  - D-007: MCP for tools, ACP for agents (Phase 3+)
- **Status**: REQ-000 (project setup) in draft. No implementation yet.
- **Next**: First Spec Writer session to create Phase 1 requirements from ARCHITECTURE.md
