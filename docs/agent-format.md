# Agent Package Format

## Directory Structure

Every agent in the marketplace follows this standard layout:

```
agents/{name}/
├── agent.yaml           # Package manifest
├── ROLE.md              # Agent instructions
├── EVOLUTION_LOG.md     # Self-correction history
├── memory/              # Persistent memory
│   ├── CONTEXT.md       # Working context, domain knowledge
│   ├── DECISIONS.md     # Decision log with rationale
│   ├── VOCABULARY.md    # Project/domain terminology
│   └── HISTORY.md       # Session history index
├── skills/evo/SKILL.md  # EVO self-evolution skill
└── templates/           # Agent-specific templates (optional)
```

## agent.yaml

The package manifest. Validated against `schemas/agent.schema.json` in ievo-sdk.

```yaml
name: spec-writer
version: "1.0.0"
description: "Turns user intent into atomic, testable specifications"
author: ievo-ai

model:
  primary: sonnet
  fallback: haiku

dependencies:
  - architect  # Required downstream agent

mcp:
  - name: filesystem
    config:
      allowed_directories: ["spec/"]

plugins: []

skills:
  - evo

hooks:
  pre_run: null
  post_run: null

disclosure:
  - "I am an AI agent in the iEvo SDD pipeline"
```

### Required Fields

| Field | Type | Description |
|-------|------|-------------|
| `name` | string | Unique agent identifier |
| `version` | string | Semver version |
| `description` | string | One-line purpose |
| `author` | string | Creator |
| `model.primary` | string | Default Claude model tier (haiku/sonnet/opus) |
| `skills` | list | Registered skill names |

### Optional Fields

| Field | Type | Description |
|-------|------|-------------|
| `model.fallback` | string | Fallback model if primary unavailable |
| `dependencies` | list | Other agents this agent depends on |
| `mcp` | list | MCP server requirements |
| `plugins` | list | Plugin dependencies |
| `hooks` | map | Pre/post run hooks |
| `disclosure` | list | Transparency statements shown to users |

## ROLE.md

The agent's instruction set. This is loaded as system context when the agent runs. Contains:

- Identity and mission
- Working rules and constraints
- Output format specifications
- Interaction patterns with other agents

## Memory Files

- **CONTEXT.md** — accumulated domain knowledge, project-specific context
- **DECISIONS.md** — numbered decision log (ID, date, decision, rationale)
- **VOCABULARY.md** — terminology definitions for consistent language
- **HISTORY.md** — table index linking to detailed session logs

## EVOLUTION_LOG.md

Records self-corrections made by the EVO skill. Each entry includes:

- Trigger (what went wrong)
- Classification (rule gap, knowledge gap, etc.)
- Root cause analysis
- Rule update applied
- Verification status
