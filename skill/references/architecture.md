# Template: .ai/ARCHITECTURE.md

---

```markdown
# Project Architecture

## Main Pattern
[Description of detected pattern, with justification extracted from real code]

## Module Structure

[Real directory tree — generate with `find` or `tree`]

## Layers and Responsibilities

| Layer | Location | Responsibility |
|-------|----------|----------------|
| [detected layer] | [real path] | [responsibility] |

## Layer Dependency Rules
- [Layer A] may depend on [Layer B]
- [Layer X] must NOT know [Layer Y]
- [Specific rule detected in code]

## Existing Modules
[Real module list found in app/modulos/ or src/]

| Module | Purpose | Known Dependencies |
|--------|---------|-------------------|
| [name] | [description] | [deps] |

## Key Architectural Decisions
[See `.ai/DECISIONS/` for the complete record]

## External Integrations
[APIs, third-party services, webhooks detected in code]
```
