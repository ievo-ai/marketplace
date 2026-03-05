# Design Patterns Catalog

Reference: https://refactoring.guru/design-patterns

Apply patterns only when they address a specific code smell. Do not force patterns.

## Creational

| Pattern | Use When |
|---------|----------|
| **Factory Method** | Polymorphic object creation needed |
| **Builder** | Complex object with many optional parameters |
| **Singleton** | Single instance required (use sparingly) |

## Structural

| Pattern | Use When |
|---------|----------|
| **Adapter** | Interface compatibility between incompatible classes |
| **Composite** | Tree structures with uniform interface |
| **Decorator** | Dynamic behavior extension without subclassing |
| **Facade** | Simplified interface to complex subsystem |

## Behavioral

| Pattern | Use When |
|---------|----------|
| **Strategy** | Interchangeable algorithms at runtime |
| **Template Method** | Algorithm skeleton with customizable steps |
| **Observer** | Event notification / pub-sub |
| **Command** | Encapsulated actions, undo/redo |
| **State** | State-dependent behavior |

## Output Format

For each applicable pattern:

```markdown
### Pattern: {PatternName}

**Current Issue:**
{description of code smell that pattern addresses}

**Proposed Solution:**
{how the pattern applies to this code}

**Before:**
```python
{current_code_snippet}
```

**After:**
```python
{refactored_code_snippet}
```

**Reference:** https://refactoring.guru/design-patterns/{pattern-name}
```
