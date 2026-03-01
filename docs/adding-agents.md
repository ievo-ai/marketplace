# Adding Agents to the Marketplace

## Steps

### 1. Create the Agent Directory

```bash
mkdir -p agents/my-agent
```

Or use ievo-sdk to scaffold:

```bash
ievo-sdk new my-agent
mv my-agent agents/
```

### 2. Create agent.yaml

Required fields: `name`, `version`, `description`, `author`, `model.primary`, `skills`.

```yaml
name: my-agent
version: "1.0.0"
description: "What this agent does in one line"
author: your-name
model:
  primary: sonnet
  fallback: haiku
dependencies: []
skills:
  - evo
```

See [agent-format.md](agent-format.md) for the full field reference.

### 3. Write ROLE.md

The agent's instruction set. Include:

- Identity and mission statement
- Working rules and constraints
- Output format (what the agent produces)
- How it interacts with upstream/downstream agents in the SDD pipeline

### 4. Add Memory Files

Create `memory/` with initial (can be empty) files:

```bash
mkdir -p agents/my-agent/memory
touch agents/my-agent/memory/{CONTEXT,DECISIONS,VOCABULARY,HISTORY}.md
```

Add headers to each file:

- `CONTEXT.md` — `# Context`
- `DECISIONS.md` — `# Decisions` + table header
- `VOCABULARY.md` — `# Vocabulary`
- `HISTORY.md` — `# History` + table header

### 5. Add EVO Skill

```bash
mkdir -p agents/my-agent/skills/evo
```

Create `skills/evo/SKILL.md` with the standard EVO skill definition: error classification, root cause analysis, rule update, verification loop.

### 6. Add EVOLUTION_LOG.md

```bash
touch agents/my-agent/EVOLUTION_LOG.md
```

Initialize with `# Evolution Log` header. Entries are added automatically by the EVO skill during agent operation.

### 7. Register in registry.yaml

Add an entry to the root `registry.yaml`:

```yaml
agents:
  # ... existing agents ...
  my-agent:
    version: "1.0.0"
    description: "What this agent does"
    tier: sonnet
    dependencies: []
```

### 8. Validate

```bash
ievo-sdk validate agents/my-agent/
```

Ensures all required files exist and `agent.yaml` passes schema validation.

### 9. Submit PR

Open a pull request to `ievo-ai/marketplace` with:

- The complete agent directory under `agents/`
- Updated `registry.yaml`
- A description of what the agent does and where it fits in the pipeline
