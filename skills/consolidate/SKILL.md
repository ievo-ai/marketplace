---
name: consolidate
description: >-
  Consolidate CLAUDE.md and linked documents: map dependency graph, find
  duplicates and contradictions, propose target structure, execute migration.
argument-hint: "<CLAUDE.md or root file>"
---

# /consolidate — Documentation Consolidation

Fixes fragmented doc systems: maps dependencies, eliminates duplication, resolves the "source of truth" ambiguity. Stops at 3 user checkpoints.

## When to Use

- CLAUDE.md references N other files and you're unsure what lives where
- The same rule appears in multiple files with slight variations
- Circular references: A → B → A
- New team member can't figure out which file to update

## Phase Overview

```
Phase 1 — Discovery      Map the full dependency graph
Phase 2 — Analysis       Duplicates, contradictions, decomposition principle
Phase 3 — Proposal       Target structure with rationale         [CHECKPOINT 1]
Phase 4 — Migration      Consolidate into new structure          [CHECKPOINT 2]
Phase 5 — Verification   No broken refs, no leftover duplicates  [CHECKPOINT 3]
```

---

## Phase 1: Discovery

**Step 1 — Collect all files**

Starting from the root file (default: `CLAUDE.md`):
1. Read the file
2. Extract all file references: `Read X.md`, `See X.md`, `X.md for ...`, `→ X.md`, markdown links `[text](path)`
3. For each referenced file: read it, extract its references
4. Repeat recursively until no new files found
5. Stop recursion on files already visited (cycle detection)

Output: flat list of all files in the graph.

**Step 2 — Build dependency graph**

For each file in the list:
- `references: [list of files this file points to]`
- `referenced_by: [list of files that point to this file]`

Identify:
- **Roots** — files with no incoming edges (entry points)
- **Sinks** — files with no outgoing edges (leaf documents)
- **Cycles** — A → B → ... → A (list every cycle found)
- **Orphans** — files that exist on disk but are not referenced anywhere

Output: dependency graph summary + cycle list.

---

## Phase 2: Analysis

**Step 3 — Content classification**

For each file, classify what content types it contains:

| Content type | Examples |
|---|---|
| `architecture` | directory trees, component descriptions |
| `conventions` | naming rules, file location rules |
| `commands` | CLI commands, bash scripts |
| `workflow` | pipelines, stage sequences |
| `agent-rules` | per-agent instructions, context loading |
| `project-state` | current version, installed agents, status |
| `external-refs` | links to repos, docs, issues |

Note files that contain **multiple content types** — these are consolidation candidates.

**Step 4 — Duplicate detection**

For every pair of files, scan for:
- **Identical blocks** — same text appears verbatim (or near-verbatim)
- **Semantic duplicates** — same rule stated differently
- **Partial overlap** — one file has a subset of what another file has

Output: duplicate inventory with file pairs and content excerpts.

**Step 5 — Contradiction detection**

For any topic that appears in 2+ files, check: do they agree?

Common contradiction patterns:
- Different counts ("12 agents" vs "17 agents")
- Different paths for the same concept
- One file says "always X", another says "X is optional"
- Stale copy that was updated in one place but not the other

Output: contradiction list with file/line references.

**Step 6 — Decomposition principle**

Infer the current organizing principle from file names and content:
- **By domain** — auth.md, payments.md, agents.md
- **By role/audience** — CLAUDE.md (agent), README.md (human), ops.md (devops)
- **By process** — spec.md, plan.md, review.md
- **By layer** — project context vs pipeline conventions vs agent rules
- **Mixed / unclear** — document what's mixed

Rate the current structure: does each file have a single clear responsibility? Are boundaries respected?

---

## Phase 3: Proposal [CHECKPOINT 1]

**Step 7 — Define target structure**

Based on the analysis, propose one of:

**Option A — Flatten**: everything in CLAUDE.md, no external refs. Good for small projects with <5 topics.

**Option B — Two-layer**: CLAUDE.md (project) + one conventions file. Good for medium projects.

**Option C — Role-based hierarchy**: files split by audience (agent vs human vs CI). No cycles by design: agents read their file + one shared file.

**Option D — Process-based hierarchy**: files split by pipeline stage. Each stage doc is self-contained.

For the recommended option, show:
```
CLAUDE.md          → what stays here (project context only)
iEVO.md            → what moves here (pipeline conventions)
agents/<name>.md   → what moves here (per-agent rules)
```

Include: what gets deleted, what gets merged, what gets created.

**CHECKPOINT 1** → present full proposal. Wait for user approval before any file changes.

---

## Phase 4: Migration

**Step 8 — Consolidate content**

For each file in the new structure:
1. Collect all content belonging to it (from all source files)
2. Deduplicate: keep the most complete/current version of each rule
3. Resolve contradictions: use the most recent source, note the decision
4. Write the consolidated file

For each file being deleted or emptied:
- Add a one-line redirect: `# Moved to X.md`
- Or delete entirely if fully superseded

**Step 9 — Fix cross-references**

After all files are written:
- Scan every file for references to old paths
- Update to new paths
- Verify no broken refs remain

**CHECKPOINT 2** → show diff summary (files created/deleted/changed). Wait for approval before finalizing.

---

## Phase 5: Verification

**Step 10 — Section inventory check (content completeness)**

Before Phase 4, extract a **section inventory** from all source files:
- For every `## Heading` and `### Subheading` in every source file, record: `file → heading → first 50 chars of content`
- After migration, verify every heading is accounted for in the new structure
- A section is "accounted for" if: (a) it appears in a new file, or (b) it was an explicit duplicate and one copy was kept

Output: table of `source section → destination file`. Flag any section with no destination as **MISSING**.

Stop migration and report if any section has no destination. Do not proceed until every section is placed or explicitly discarded by the user.

**Step 11 — Graph re-check**

Re-run Phase 1 on the new structure:
- No cycles
- No orphans (unless intentional)
- Every referenced file exists

**Step 12 — Duplicate re-check**

Re-run Step 4 on new structure: zero duplicates.

**Step 13 — Single source of truth audit**

For each content type identified in Step 3, confirm: it lives in exactly one file now.

**CHECKPOINT 3** → present final report:
```
Files before:   N
Files after:    M
Sections total: S   (tracked from Step 10)
Sections moved: S   (must equal total — zero missing)
Duplicates removed: K
Contradictions resolved: J
Cycles broken: C
```

## Anti-Pattern Detection

Stop and warn if:
- A new file is created that references back to a file that references it (new cycle)
- Content is moved but not removed from the source (new duplicate created)
- A file ends up containing 3+ content types after migration
- Migration is executed without CHECKPOINT 1 approval
- Section inventory (Step 10) has any MISSING entries — never proceed past this
