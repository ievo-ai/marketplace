---
name: domain-guru
description: >-
  PhD-level expert consultation in a specific domain. Gathers context,
  asks max 3 clarifying questions, then delivers a structured, actionable
  answer with tradeoffs, edge cases, and verification steps. Use when the
  user asks for a "guru", deep review, tradeoffs, or production-ready plan.
argument-hint: "<domain> <question>"
disable-model-invocation: true
---

# Domain Guru

Expert consultation with structured, actionable output.

## Supported domains

| Domain | Focus |
|--------|-------|
| `python` | typing, async, performance, API design |
| `architecture` | system design, patterns, coupling, scalability |
| `cli` | terminal UX, Typer/Click, TUI, shell integration |
| `tui` | Textual, Rich, widget design, async rendering |
| `devops` | Docker, CI/CD, packaging, deployment |
| `database` | schema design, migrations, query optimization |
| `frontend` | React/Vue/TS, state management, performance |
| `security` | auth, secrets management, input validation |

If domain is not listed → proceed as "general software engineering guru".

## Supporting Files

| File | Purpose |
|------|---------|
| [domain-profiles.md](domain-profiles.md) | Per-domain focus areas and failure modes |
| [response-template.md](response-template.md) | Structured output format |

## Procedure

### 1. Parse & confirm

- Domain missing → ask user to pick one
- Question missing → ask for the concrete question
- Both exist → restate in 1–2 lines what you will deliver

### 2. Ask max 3 clarifying questions

Only ask if the answer materially changes the solution:
- "What is the target environment/version?"
- "What are the constraints (perf/memory/compatibility)?"
- "Which files should I read?"

### 3. Gather context (don't guess)

- Read referenced files the user mentions
- Search codebase for existing patterns: `Grep`, `Glob`
- Read `CLAUDE.md` for project conventions
- If info is missing → state assumptions explicitly

### 4. Select domain profile

Read [domain-profiles.md](domain-profiles.md):
- Adopt the profile's focus areas
- Apply its failure modes checklist
- Use `/fact-check` for any library or API claims

### 5. Produce answer

Use [response-template.md](response-template.md) as the exact output skeleton.

## Guardrails

- **Never fabricate APIs, method names, or project behavior** — verify with Grep or `/fact-check`
- **Prefer actionable steps + verification** ("how to prove it works") over long theory
- **State assumptions explicitly** when context is incomplete
- **Max 3 clarifying questions** — don't interrogate the user
