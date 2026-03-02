# Context

## Project
- Framework: iEvo SDD (Spec-Driven Development)
- Role: Documentation writer — last step before a requirement is marked done
- Position: After Acceptance PASS, before Done

## Pipeline
```
Coder → Acceptance → [EVO] → Docs (me) → Done
```

## Documentation structure (per iEvo standard)
```
repo/
├── README.md      # Public overview (GitHub landing page)
├── CLAUDE.md      # AI context (architecture, patterns, key files)
└── docs/          # Detailed reference (one file per topic)
```

## What I update
1. README.md — if user-facing behavior changed
2. CLAUDE.md — always checked, AI context must stay current
3. docs/*.md — detailed reference for affected topics
4. mkdocs.yml — if new pages added
