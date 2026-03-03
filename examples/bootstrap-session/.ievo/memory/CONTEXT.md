# Project Context

<!-- Updated by Spec Writer agent at the end of each session -->

## Project Name
iEvo (ievo.ai) — Self-Evolving Multi-Agent SDD Framework

## Project Description
A self-evolving multi-agent framework with agent marketplace.
Three repos: ievo-marketplace (agents), ievo-sdk (dev template), ievo-cli (CLI).
Agents learn from mistakes via EVO skill, feed improvements back to marketplace.
Genetic algorithm applied to agent evolution for quality assurance.

## Tech Stack
- Python 3.11+ (CLI, orchestrator, agent wrappers)
- Agent marketplace (ievo-marketplace repo, agent.yaml packages)
- Copier (Dev SDK for creating new agents, NOT for project init)
- MCP (agent↔tools communication)
- ACP (agent↔agent communication, future Phase 3+)
- Markdown files (specs, memory, configuration)
- pytest (test runner)

## Current State
- Total requirements: 1 (REQ-000 project setup, draft)
- Implemented: 0
- In progress: 0
- Blocked: 0
- Architecture document: ARCHITECTURE.md (complete, 12 sections)
- Domain: ievo.ai (purchased)
- Research: competitive landscape analyzed

## Key Entities / Components
- **3 repos**: ievo-marketplace, ievo-sdk, ievo-cli
- **Agents**: Spec Writer, Architect, Coder (Phase 1), Tester/PM/Reviewer (future)
- **EVO skill**: Self-evolution — every agent has it, logs to EVOLUTION_LOG.md
- **Curator agent**: Reads evolution logs from all projects, updates marketplace agents
- **Genetic testing**: Eval suites per agent, fitness scoring, mutation selection
- **agent.yaml**: Package manifest (deps, version, model, hooks, MCP, plugins)
- **Memory**: agents/<role>/memory/ — persistent across sessions
- **Onboarding**: Spec Writer fills its own memory on first session (no pre-warming)

## Architecture Notes
- Build SDD methodology layer, NOT another orchestrator
- Marketplace with `ievo add <agent>` — pip-like dependency resolution
- Copier only in Dev SDK for agent creators
- EVO + Genetic Algorithm = agents self-improve and quality is tested
- 3-tier model routing: Opus → Sonnet → Haiku
- Progressive disclosure for agent prompts
- File-based memory now, SQLite later
- See ARCHITECTURE.md for full details
