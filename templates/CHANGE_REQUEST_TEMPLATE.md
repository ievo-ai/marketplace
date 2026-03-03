# CR-XXX: <Title>

## Metadata
- **Modifies:** REQ-XXX
- **Source:** GitHub Issue #N
- **Status:** draft | impact-review | ready | applied
- **Created:** <date>
- **Applied:** <date or empty>

## What Changes

<!-- Quote the EXACT current acceptance criteria being modified, then show the new version -->

### Modified criteria

**Old (REQ-XXX, criterion N):**
```
<exact current text>
```

**New:**
```
<new text>
```

### New criteria added
- [ ] `<new acceptance criterion>`
- [ ] `<new acceptance criterion>`

### Criteria removed
- ~~`<criterion being removed>`~~ — Reason: <why>

## What Stays the Same

<!-- Explicitly list behaviors that are NOT changing. This prevents the agent
     from accidentally breaking things that should remain stable. -->

- <behavior 1> — unchanged
- <behavior 2> — unchanged

## Impact Estimate

<!-- Filled by the Coder Agent during impact-review phase -->

### Tests affected
| Test file | Action | Details |
|-----------|--------|---------|
| | modify | |
| | delete | |
| | create | |

### Code affected
| Source file | Action | Details |
|-------------|--------|---------|
| | modify | |

### Dependent requirements to recheck
| REQ | Status | Risk |
|-----|--------|------|
| | implemented | <what might break> |

### Cascade CRs created
<!-- Filled after implementation if dependent REQ tests break -->
- CR-YYY for REQ-ZZZ — <reason>

---

<!--
RULES FOR CHANGE REQUESTS:
1. Always quote exact current text being changed
2. Always list what stays the same
3. Impact estimate is filled by the agent, not by you
4. CR with status != ready → agent skips it
5. CRs are ALWAYS prioritized over new REQs
6. Agent NEVER auto-fixes cascade breakages — creates new CRs instead
-->
