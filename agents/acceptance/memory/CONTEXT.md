# Context

## Project
- Framework: iEvo SDD (Spec-Driven Development)
- Role: Final quality gate in pipeline
- Position: After Coder, before marking requirement as implemented

## Pipeline
```
User → Spec Writer → Architect → Coder → Acceptance (me) → Done
```

## Key files I read
- `spec/SPEC_INDEX.md` — find requirements in "review" status
- `spec/requirements/REQ-xxx.md` — acceptance criteria
- `plans/PLAN-REQ-xxx.md` — intended architecture
- Source code + test files — actual implementation

## What I verify
1. Every acceptance criterion has code + test
2. Tests verify real outcomes, not just mock calls
3. All test types present (unit, integration, edge cases)
4. Coverage on changed files is 100%
5. Docs updated if user-facing change
