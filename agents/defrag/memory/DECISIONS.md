# Defrag Decisions

## D-001: Rule ownership principle (2026-03-02)

Rules live where they're enforced. Each rule has ONE primary owner — the agent whose responsibility aligns with the rule. Eva CLAUDE.md is a meta-document, not a rule dump.

## D-002: Read-only by design (2026-03-02)

Defrag never modifies files. It produces reports. Eva or human acts on findings. This prevents cascading edits from a cheap model making mistakes.

## D-003: Severity levels (2026-03-02)

- HIGH: rule missing from its enforcing agent's ROLE.md
- HIGH: stale reference (broken link/path)
- MEDIUM: rule drift (different wording across files)
- MEDIUM: doc overlap (duplicate content)
- LOW: orphan rule (exists in child, not tracked by parent)
- LOW: missing optional doc
