# Template: .ai/CONVENTIONS.md

---

```markdown
# Code Conventions

## Naming

| Element | Convention | Example |
|---------|-----------|---------|
| Classes | [detected] | [example] |
| Methods | [detected] | [example] |
| Variables | [detected] | [example] |
| Files | [detected] | [example] |
| DB tables | [detected] | [example] |

## Code Style
[Extracted from .editorconfig, .prettierrc, .php-cs-fixer.php, .eslintrc]

- **Indentation**: [spaces/tabs, size]
- **Line endings**: [LF/CRLF]
- **Max line length**: [if configured]
- **Quotes**: [single/double]

## Commit Format
[Extracted from .commitlintrc.json or commitlint.config.js]

```
[type](scope): description

Types: [list detected types]
```

## Static Analysis
[Extracted from phpstan.neon / mypy.ini / tsconfig.json]

- **Tool**: [e.g. PHPStan level 8, mypy strict, tsc --strict]

## File Organization
[Detected patterns: where to put new classes, services, tests, etc.]

## Documentation Standards
[PHPDoc / JSDoc / docstrings — format detected in code]
```
