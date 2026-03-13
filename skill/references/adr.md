# Template: .ai/DECISIONS/[YYYY-MM-DD]-NNN-[title].md

File naming: `YYYY-MM-DD` = decision date, `NNN` = sequential number (001, 002…),
`[title]` = kebab-case short title.

Example: `2024-03-15-001-json-file-persistence.md`

---

```markdown
# [NNN]: [Decision Title]

**Date**: [YYYY-MM-DD]
**Status**: Accepted | Proposed | Superseded by NNN

## Context
[What problem or need motivated this decision — inferred from code]

## Decision
[What was decided to implement]

## Consequences

**Positive:**
- [consequence]

**Negative / Trade-offs:**
- [consequence]

## Discarded Alternatives
1. **[Alternative]**: [why it wasn't chosen]

## Related Files
- [Real paths in the project]
```

---

## ADRs to auto-generate

Create one ADR for each significant decision detectable from the code:

| Condition | Suggested ADR title |
|-----------|---------------------|
| DDD / Clean Architecture detected | `NNN-domain-driven-design-architecture` |
| JsonQ detected | `NNN-json-file-persistence` |
| Monorepo detected | `NNN-monorepo-structure` |
| Multiple languages coexisting | `NNN-multilanguage-stack` |
| Custom framework (no standard one) | `NNN-custom-framework-decision` |
| Module-scoped tests | `NNN-encapsulated-module-testing` |
| Specific ORM or query builder | `NNN-[orm-name]-as-persistence-layer` |

Generate only the ADRs supported by actual evidence in the codebase.
