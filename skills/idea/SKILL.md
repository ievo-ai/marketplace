# /idea — Quick Idea Capture

Capture an idea into `.ievo/tasks/` as a new task with `status: idea`. No ceremony — just get it written before it's lost.

## Usage

```
/idea <idea in any form>
```

## Workflow

1. **Read** `.ievo/tasks/_index.csv` to find the next task number
   - If no tasks exist → start at 001
   - Find the highest existing ID → increment

2. **Create** `.ievo/tasks/NNN/spec.md`:

```markdown
---
id: "NNN"
title: <title>
type: idea
status: idea
priority: medium
deps: []
pr: null
stage: null
attempts: 0
created_session: null
source: user
---

# <title>

## Idea

<captured text — clean up grammar but preserve intent>

## Why

<1-2 sentences: what problem does this solve or what value does it add?>
```

3. **Update** `.ievo/tasks/_index.csv` — append a new row

4. **Confirm** — print the task path and one-line summary. Nothing else.

## Rules

- **Speed over polish.** This is a capture tool, not a spec writer. 30 seconds max.
- **Preserve intent.** Clean up grammar but don't rewrite the idea. User's words matter.
- **No duplicates.** Quickly scan `_index.csv` — if something very similar exists, mention it instead of creating a duplicate.
- **Status: idea.** Tasks start as `idea`. Spec-writer refines them to `ready` with user approval.
- **No evaluation.** Don't judge the idea. Don't add pros/cons. Just capture it.
