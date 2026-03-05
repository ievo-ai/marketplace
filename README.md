```
 ██╗ ███████╗██╗   ██╗ ██████╗
 ╚═╝ ██╔════╝██║   ██║██╔═══██╗
 ██╗ █████╗  ██║   ██║██║   ██║
 ██║ ██╔══╝  ╚██╗ ██╔╝██║   ██║
 ██║ ███████╗ ╚████╔╝ ╚██████╔╝
 ╚═╝ ╚══════╝  ╚═══╝   ╚═════╝
```

# iEvo Marketplace

Agent registry for the iEvo self-evolving SDD framework. Install agents like packages — they learn from every mistake.

## Available agents

| Agent | Model | Description |
|-------|-------|-------------|
| **spec-writer** | sonnet | Features → atomic, testable requirements |
| **architect** | opus | REQs → implementation plans with TDD strategy |
| **team-lead** | sonnet | Plans → TDD code following spec and architecture |

## Usage

```bash
pip install ievo
ievo init my-project
cd my-project
ievo add spec-writer architect team-lead
ievo run spec-writer
```

## Self-evolution

Every agent includes the EVO skill. When an agent makes a mistake, it analyzes the root cause and updates its own ROLE.md — permanently improving.

Three levels of evolution:
1. **EVO** — agent learns from its own mistakes (local)
2. **Curator** — aggregates lessons across projects → improves marketplace agents
3. **Eva** — scans external signals → improves the platform itself

## Links

- [ievo.ai](https://ievo.ai)
- [CLI](https://github.com/ievo-ai/cli)
