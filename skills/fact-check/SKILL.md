---
name: fact-check
description: >-
  Verifies software facts to prevent hallucinations: PyPI packages, GitHub
  repos, library APIs, CLI flags, and version numbers. Auto-invokes when
  about to recommend a library, reference a GitHub repo, or use an API method
  that hasn't been verified in this session. Also use manually via /fact-check.
argument-hint: "[library, repo URL, API method, or claim]"
---

# Fact Check

Verify before writing. Prevent hallucinated packages, invented APIs, and non-existent repos.

## Primary tool: WebSearch

**Always use WebSearch first.** It returns cited sources — use those sources as evidence.
Search queries must be specific enough to confirm or deny the exact claim.

Examples:
- `"httpx python library pypi"` → confirms existence, finds PyPI page
- `"textual python tui github stars 2025"` → confirms repo stats
- `"typer add_argument method does not exist"` → surfaces corrections
- `"python uv package manager changelog 0.5"` → verifies version

**After WebSearch**: if the claim is still ambiguous, fall back to direct fetch (WebFetch) or Bash.

## When to activate

Trigger automatically when you encounter ANY of:
- Recommending a **Python package** to install or use
- Referencing a **GitHub repository** with star counts or activity claims
- Using a **library API method** not seen in current session's file reads
- Citing a **version number** or **changelog entry**
- Making a claim about a **CLI flag or command** syntax

Also available manually: `/fact-check "library or claim"`

## Verification workflows

### A. Verify a PyPI package

1. `WebSearch: "{package} pypi python"` — confirm it appears on pypi.org
2. `WebFetch: https://pypi.org/pypi/{package}/json` — get canonical metadata
3. Verify: real name, latest version, last release date
4. **Maintenance check**: last release >2 years ago → flag ⚠️, suggest alternative
5. **If package doesn't exist** → do NOT suggest it. WebSearch for real alternative.

### B. Verify a GitHub repository

1. `WebSearch: "{owner}/{repo} github"` — confirm it appears in results
2. `WebFetch: https://github.com/{owner}/{repo}` — check it resolves, read description
3. Verify: name, owner, last commit date, star count from the page
4. **Never invent star counts** — read from the fetched page
5. **If repo doesn't exist** → remove the reference entirely

### C. Verify a library API method

1. `WebSearch: "python {lib} {method} docs"` — find official docs page
2. `WebFetch` the docs page — confirm the method exists and read its signature
3. Or run: `uv run python -c "import {lib}; help({lib}.{method})"` via Bash
4. **If method doesn't exist** → do NOT use it. Find the real method from docs.
5. **Never assume** method signatures — always verify

### D. Verify a CLI command or flag

1. Run `{command} --help` via Bash — check flag appears in output
2. If command not installed: `WebSearch: "{command} {flag} cli docs"`
3. **If flag doesn't exist** → use correct flag from help output

### E. Verify during research

When the researcher agent produces findings:
1. For every package mentioned → run workflow A
2. For every GitHub repo → run workflow B
3. Flag unverified items with `⚠️ TODO: verify` in research files
4. Do NOT record unverified facts in `.ievo/research/` files as confirmed

## Output format

```
## Fact Check: [subject]

**Claim**: [what was claimed]
**Verdict**: ✅ Confirmed | ⚠️ Stale/partial | ❌ Does not exist | ❓ Unverified

**Evidence**: [search result URL or fetched page]

**Action**: [proceed / use alternative X / ask user]
```

## Rules

- **WebSearch first** — always search before fetching or running commands
- **Cite sources** — every verdict must have a URL or command output as evidence
- **Never suggest a package you haven't verified exists on PyPI**
- **Never cite a GitHub repo without checking the URL resolves**
- **Never use an API method without verifying it in docs or source**
- **Flag, don't silently drop** — if something doesn't check out, tell the user
