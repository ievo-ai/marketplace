# Evolution Convention

> How the iEvo pipeline accumulates and propagates lessons across sessions.

## Directory Structure

All evolution files live in `.ievo/evolution/`:

```
.ievo/evolution/
├── LOG.md              ← append-only findings journal (write-only, NOT loaded as context)
├── KERNEL.md           ← kernel overlay: pipeline-level lessons (read by ALL agents)
└── agents/
    └── <agent>.md      ← per-agent overlay: agent-specific lessons (read by that agent)
```

**Read rules:**
- `LOG.md` — **never** loaded as context by agents. Only the Evolution agent writes to it.
- `KERNEL.md` — loaded by **all agents** at session start (read if exists).
- `agents/<agent>.md` — loaded by **that agent** at session start (read if exists).

---

## LOG.md — Findings Journal

`LOG.md` is the chronological record of all evolution findings. It is written by the Evolution agent after every analysis. No agent loads it as context — it is write-only from an agent's perspective.

### Entry format

```markdown
## YYYY-MM-DD: <brief title>

**Trigger:** <POST-SPEC|POST-PLAN|POST-IMPLEMENTATION|POST-ACCEPTANCE|RETRY-EXHAUSTED>
**Agent:** <which agent's output was analyzed>
**Confidence:** <low|medium|high>

**Finding:** <1-2 sentences describing what happened>
**Root cause:** <trace to the earliest pipeline point where this could have been caught>
**Proposed mutation:** <target agent or kernel> — <rule change summary>

**Issue:** <GitHub issue URL>
```

### Rules

- **Append-only.** Never edit or delete entries — they are the permanent finding history.
- **Number sequentially** in commit messages and cross-references (E-001, E-002…) for traceability.
- **Always include the Issue URL** after filing with curator. If not yet filed, mark `TODO`.
- **Full detail here.** LOG.md is private — write complete context, code references, root cause chains.

---

## Overlays — Actionable Rules

Overlays distill findings into concise, actionable rules loaded as context at every session start.

### KERNEL.md

Contains pipeline-level lessons — rules that apply to **all agents**. Written when a finding's root cause is in pipeline conventions, document lifecycle rules, naming conventions, or cross-agent coordination patterns.

### agents/\<agent\>.md

Contains agent-specific lessons — rules that apply only to one agent. Written when a finding's root cause is in that agent's own instructions or behavior.

### Entry format

```markdown
# Evolution: <agent-name|KERNEL>

## YYYY-MM-DD: <brief title>

**Type:** <spec-error|plan-error|code-error|test-error|process-error>
**What happened:** <1-2 sentences>
**Root cause:** <why it happened>
**Lesson:** <actionable rule to prevent recurrence>
```

### Rules

- **Overlay, not override.** Overlay files ADD rules — they never contradict base agent instructions.
- **Project-specific only.** Generic lessons belong in the curator. Only project-specific rules here.
- **Append-only.** Never delete entries — they are the learning history.
- **Survives marketplace updates.** When HR updates an agent from the marketplace, overlays are preserved.
- **One entry per finding.** Each E-NNN finding produces at most one overlay entry.

---

## Routing

```
Finding in agent behavior        → LOG.md (log) + agents/<agent>.md (rule)
Finding in pipeline conventions  → LOG.md (log) + KERNEL.md (rule)
All findings                     → curator GitHub issue (ievo-ai/curator, label: evolution_log)
```

The Evolution agent decides the target after root cause analysis:

- Root cause in agent's own instructions or behavior → `agents/<agent>.md`
- Root cause in pipeline rules (IEVO.md conventions, naming, lifecycle) → `KERNEL.md`

When in doubt — if the finding applies broadly to how all agents should behave — it belongs in `KERNEL.md`.

---

## Context Loading Template

Each agent's Context Loading section must include:

```
5. `.ievo/evolution/agents/<agent-name>.md` — local evolution rules (if exists)
6. `.ievo/evolution/KERNEL.md` — kernel evolution overlay (read if exists)
```

Load both files unconditionally at session start. If a file does not exist, skip silently.
