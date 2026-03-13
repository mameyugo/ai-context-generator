# Template: .ai/TESTING.md

---

```markdown
# Testing Strategy

## Detected Frameworks
- **Unit**: [e.g. PHPUnit 11]
- **BDD / Integration**: [e.g. Behat 3.x with Gherkin in Spanish]
- **E2E**: [if present: Playwright, Cypress, Panther]
- **Static analysis**: [e.g. PHPStan level 8]

## Test Location — CRITICAL RULE
[Describe the real detected policy. Example for encapsulated modules:]

Tests are encapsulated inside each module, NOT in central folders:

✅ Correct:
```
app/modulos/{moduleName}/Test/
├── Integration/
│   └── ModuleNameApiTest.php
└── Unitaries/
    └── ServiceNameTest.php
```

❌ Incorrect:
```
Tests/Integration/  ← Do not use
tests/unitaries/    ← Do not use
```

## Detected Commands

```bash
# Extracted from composer.json scripts or Makefile
[real command]    # description
[real command]    # description
```

## Testing Patterns
- **Mocks**: [how they're used in this project]
- **Fixtures**: [real location and format]
- **Factories**: [if they exist]
- **Setup / Teardown**: [detected hooks]

## Minimum Coverage Required
[If configured — extract from phpunit.xml or jest.config]

## BDD Scenarios (if applicable)
[Detected language and convention — e.g. Gherkin in Spanish]
```
