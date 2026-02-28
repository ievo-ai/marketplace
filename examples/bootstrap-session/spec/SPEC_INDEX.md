# Specification Index

## Selection Algorithm

```
FIRST: Check for Change Requests (CRs) with status: ready → process those first
THEN:  Select requirements using:
  1. Filter: status = ready
  2. Filter: all dependencies have status = implemented
  3. Score using PRIORITY.md formula
  4. Select highest score
  5. Tiebreak: lower REQ number (older first)
```

See PRIORITY.md for full scoring details.

## Requirements Registry

<!-- Keep this in sync with requirement files. Agent updates on every status change. -->

| ID | Title | Status | Version | Priority | Dependencies | Blocks | Questions | Source |
|----|-------|--------|---------|----------|--------------|--------|-----------|--------|
| REQ-000 | Project Setup | ready | 1 | critical | none | all | 0 | — |

## Change Requests

<!-- CRs are ALWAYS processed before new REQs -->

| ID | Modifies | Status | Created | Source |
|----|----------|--------|---------|--------|

## Status Legend

### Requirement statuses
- `draft` — has ambiguities, not ready for implementation
- `ready` — fully specified, agent can pick it up
- `blocked` — agent found ambiguities, questions filed
- `in-progress` — agent is currently implementing
- `implemented` — all acceptance criteria met, all tests passing
- `removed` — deleted via Change Request

### Change Request statuses
- `draft` — CR written but not reviewed
- `impact-review` — agent assessed impact, waiting for human review
- `ready` — approved for implementation
- `applied` — changes merged into REQ, done
- `rejected` — decided not to apply

## Dependency Rules

- Agent MUST NOT start a REQ whose dependencies are not ALL `implemented`
- Circular dependencies are a spec error → file a question
- `REQ-000` (project setup) has no dependencies and blocks everything else
- CRs have implicit dependency on their target REQ being `implemented`

## Source Tracking

<!-- Map requirements back to their origin -->
<!-- | REQ-001..003 | GitHub Issue #12 | -->
