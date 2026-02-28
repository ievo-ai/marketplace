# CONTEXT

## System Under Research

iEvo — a self-evolving multi-agent SDD (Specification-Driven Development) framework.

### Key Components
- **CLI** (`ievo`): project management, agent orchestration, TUI dashboard
- **Marketplace**: agent registry (spec-writer, architect, coder, researcher)
- **SDK**: agent development toolkit
- **Eva**: meta-evolution mother agent (Level 3)
- **Curator**: cross-agent pattern detection (Level 2)

### Architecture
- Agents run via Claude Code CLI with ROLE.md as system prompt
- Persistent memory: CONTEXT, DECISIONS, VOCABULARY, HISTORY per agent
- SDD pipeline: User → Spec Writer → Architect → Coder → Tester → Reviewer
- 3-tier evolution: EVO (local) → Curator (cross-agent) → Eva (platform)
- MCP servers and Claude Code plugins for external tool access

### Research Focus Areas
- Multi-agent coordination patterns
- Self-improving AI systems
- Specification-driven development
- Code generation quality and TDD
- Agent memory and learning
- MCP ecosystem growth
