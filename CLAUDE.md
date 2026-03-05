# iEvo Marketplace

Agent registry for the iEvo self-evolving SDD framework.

## Structure

```
marketplace/
├── registry.yaml              # Index: all agents, versions, deps
├── agents/
│   ├── spec-writer/           # Requirements analyst
│   │   ├── agent.yaml         # Manifest (version, model, deps, hooks)
│   │   ├── ROLE.md            # Agent instructions (progressive disclosure)
│   │   ├── memory/            # Empty templates (filled per-project)
│   │   ├── skills/evo/        # Self-evolution skill
│   │   ├── templates/         # REQ/Q templates
│   │   └── EVOLUTION_LOG.md   # Empty (grows per-project)
│   ├── architect/             # Technical planner
│   └── coder/                 # TDD implementer
```

## How it works

1. `ievo add spec-writer` → CLI reads `registry.yaml`, finds agent
2. Downloads agent dir to project's `agents/spec-writer/`
3. Resolves dependencies (architect needs spec-writer)
4. Creates empty memory files for the project
5. Agent is ready to run: `ievo run spec-writer`

## Agent package format

Each agent has:
- `agent.yaml` — manifest (name, version, model tier, deps, hooks, disclosure tiers)
- `ROLE.md` — instructions structured as Metadata → Instructions → Resources
- `memory/` — CONTEXT.md, DECISIONS.md, VOCABULARY.md, HISTORY.md (templates)
- `skills/evo/SKILL.md` — self-evolution skill (same for all agents)
- `EVOLUTION_LOG.md` — starts empty, grows as agent learns

## Adding a new agent

1. Create dir in `agents/<name>/`
2. Write `agent.yaml` (copy from existing agent, modify)
3. Write `ROLE.md` with three sections: Metadata, Instructions, Resources
4. Copy `skills/evo/SKILL.md` from any other agent
5. Create empty `memory/` templates
6. Add entry to `registry.yaml`
7. PR and merge

## Core agents (Phase 1)

| Agent | Model | Role |
|-------|-------|------|
| spec-writer | sonnet | Features → atomic REQs |
| architect | opus | REQs → implementation plans |
| team-lead | sonnet | Plans → TDD code |

## Conventions

- Versions: semver (0.1.0)
- ROLE.md: three progressive disclosure tiers (metadata/instructions/resources)
- Memory files: markdown, git-tracked, filled by agent during sessions
- EVO skill: identical across agents, lives in `skills/evo/SKILL.md`
