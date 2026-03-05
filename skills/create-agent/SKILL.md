---
name: create-agent
description: >-
  Creates a new Claude Code agent from a user prompt. Searches for existing
  agents to avoid duplication, asks clarifying questions to narrow scope,
  researches official docs and best practices, then produces a deployment-ready
  .md file. Use when the user asks to "create an agent", "build an agent", or
  "I need an agent that...".
argument-hint: "[agent description or purpose]"
---

# Create Agent

Build a specialized, deployment-ready Claude Code agent from a user description.

## Phases

---

### Phase 0: Parse input

Extract from the user's request:
- **Purpose**: what task does the agent do?
- **Domain**: what technology/framework does it specialize in?
- **Trigger**: when should Claude invoke it automatically?
- **Scope**: broad ("Python developer") or narrow ("FastAPI specialist")?

If purpose is missing → ask before continuing.

---

### Phase 1: Duplicate detection

Search existing agents:
```bash
ls .claude/agents/*.md
ls src/ievo/marketplace/agents/*.md 2>/dev/null
```

Read the `description:` field of each. Find semantic overlap with the requested agent.

**If a similar agent exists:**

Present clearly:
```
Found: <name> — "<description>"

Options:
A) Use this agent as-is
B) Specialize it further (narrow scope — ask more questions)
C) Improve the existing agent (extend capabilities)
D) Create a separate agent for a distinct use case
```

Wait for user choice before proceeding.

**If no similar agent exists** → proceed to Phase 2.

---

### Phase 2: Clarifying questions (max 5)

Ask only questions that materially change the agent's behavior:

1. **Scope**: broad tool ("Python developer") or narrow specialist ("FastAPI endpoint design")?
2. **Primary task**: what is the ONE thing this agent does better than anyone else?
3. **Input**: what does the user hand to this agent? (code file, requirement, error message?)
4. **Output**: what does the agent produce? (code, spec, report, review?)
5. **Tools needed**: does it need to write files? Run bash? Search the web?

For narrow-domain agents (FastAPI, SQLAlchemy, Celery, etc.) — also ask:
- Which version to target?
- Any project-specific conventions to follow?

---

### Phase 3: Deep research

For domain-specific agents, research before writing:

1. **Official docs** — `WebSearch: "{framework} official documentation {year}"` → `WebFetch` the docs
2. **Best practices** — `WebSearch: "{framework} best practices production {year}"`
3. **Common pitfalls** — `WebSearch: "{framework} common mistakes anti-patterns"`
4. **Verify all findings** with `/fact-check` before including in agent instructions

Summarize research into:
- Key concepts the agent must know
- The #1 rule for this domain (the thing beginners always get wrong)
- The docs URL the agent should read at session start

---

### Phase 4: Design the agent

Based on research and clarifying answers:

**Name**: lowercase, hyphens, specific (`fastapi-specialist` not `python-developer`)

**Description** (critical — this is the auto-invoke trigger):
- 3rd person, max 1024 chars
- Include WHAT it does + WHEN to invoke it
- Be specific: "FastAPI endpoint design" not "helps with FastAPI"
- Test mentally: "Would Claude call this agent for request X?" — if unsure, rewrite

**Model selection**:
- `opus` — architecture decisions, complex analysis, research-heavy tasks
- `sonnet` — implementation, code review, most tasks (default)
- `haiku` — simple, fast, repetitive tasks

**Tools** — only what's needed:

`AskUserQuestion` is included in ALL agents by default. Only omit it if the agent is explicitly non-interactive (e.g., a pure pipeline step that must never pause for user input).

| Need | Tools |
|------|-------|
| Read code | Read, Glob, Grep |
| Write code | Write, Edit |
| Run commands | Bash |
| Search web / verify facts | WebSearch, WebFetch |
| Create files | Write |

**Fresh docs rule** — for framework agents, replace `{framework_docs_line}` in Context Loading with:
```
5. **{framework} docs** — WebFetch {docs_url} for the specific feature being worked on
```
For non-framework agents, remove the `{framework_docs_line}` placeholder entirely.

---

### Phase 5: Write the agent

Follow the standard agent format:

```markdown
---
name: {name}
description: >
  {description — specific, 3rd person, includes WHAT + WHEN}
model: {sonnet|opus|haiku}
tools:
  - {only tools actually needed}
---

# {Title}

> {one-line role summary}

## Context Loading

**FIRST — read these files before doing anything:**
1. `.ievo/memory/CONTEXT.md` — project context
2. `.ievo/memory/DECISIONS.md` — architectural decisions
3. `.ievo/evolution/agents/{name}.md` — local evolution rules (if exists)
4. `.ievo/evolution/KERNEL.md` — kernel evolution overlay (if exists)
{framework_docs_line}

**LAST — save your memory before ending EVERY session:**
1. `.ievo/memory/CONTEXT.md` — updated findings
2. `.ievo/memory/HISTORY.md` — session summary
3. Your agent memory — personal learnings that apply across projects

## Role & Responsibilities

{what the agent does, what it does NOT do}

## Workflow

{step-by-step instructions}

## Rules

{numbered, actionable rules}

## Evolution

When you make a mistake or discover a project-specific pattern:
- Update `.ievo/evolution/agents/{name}.md` with the lesson
- Format: date, context, action, goal
```

---

### Phase 6: Quality validation

Before presenting to user, self-check:

**Description test**: read the description aloud. Would Claude invoke this agent for a relevant request? Is it specific enough to not conflict with other agents?

**Tools audit**: is every listed tool actually used in the workflow? Remove unused tools.

**Minimal principle**: does the agent do ONE thing well? If it does 3+ unrelated things → split.

**Fresh docs check**: for any framework mentioned, is there a "WebFetch docs before starting" instruction?

**Anti-hallucination check**: does the agent instruct to use `/fact-check` for any library recommendations?

---

### Phase 7: Deploy

**Detect marketplace:**
- Check if `src/ievo/marketplace/agents/` exists

**If marketplace found:**
1. Write agent to `src/ievo/marketplace/agents/{name}.md`
2. Symlink `.claude/agents/{name}.md` → marketplace source
3. Add entry to marketplace registry if it exists

**If marketplace NOT found:**
Ask user:
1. Deploy to `.claude/agents/{name}.md` directly
2. Specify a custom path (and notify user to update this skill's deploy logic)

---

### Phase 8: Preview test

Show user a test invocation:

```
Test prompt: "{example request that should trigger this agent}"
Expected: Claude invokes {name} automatically

Try it: paste the test prompt and see if Claude routes to this agent.
```

Ask: "Does this match what you expected? Should we adjust the description or scope?"

---

## Anti-patterns

- **Too broad**: "Python developer" — use "FastAPI endpoint specialist" instead
- **Too many tools**: list only what the workflow actually uses
- **No fresh docs rule**: framework agents without doc-reading instruction will hallucinate stale APIs
- **Vague description**: "helps with coding" — never triggers automatically
- **Copying base agent**: new agent must add value beyond what existing agents already do
