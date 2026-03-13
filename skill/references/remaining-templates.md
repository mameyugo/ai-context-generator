# Templates: Remaining .ai/ Files

---

## .ai/DESIGN-SYSTEM.md

```markdown
# UI Design System

## UI Framework & Version
[Detected — e.g. Bootstrap 5.3, Tailwind CSS 3.4, AdminLTE 3.2]

## Template Engine
[Detected — e.g. Twig, Blade, JSX, Vue SFC]

## Component Structure
[Real paths where UI components live]

## Color Palette
[Extracted from CSS variables, tailwind.config, or SCSS variables]

## Typography
[Font families, sizes, scale detected in stylesheets]

## Spacing & Grid
[System detected — e.g. Bootstrap 12-col, Tailwind spacing scale]

## Reusable Components
[List of components found in the project]

| Component | Location | Usage |
|-----------|----------|-------|
| [name] | [path] | [when to use] |

## Icons
[Icon library detected — e.g. Font Awesome 6, Heroicons, custom SVG]

## Rules for New UI
- [ ] Use existing components before creating new ones
- [ ] Follow the detected color palette
- [ ] [Other project-specific rule]
```

---

## .ai/I18N.md

```markdown
# Internationalization

## Supported Languages
[Detected — e.g. Spanish (es) and Galician (gl)]

## Translation System
[Detected — e.g. YAML files in /locales, lang() function, Symfony Translator]

## Translation File Structure
[Real tree detected]

## Key Conventions
[Detected pattern — e.g. module.entity.field or module.action.description]

## Regional Formats
- **Dates**: [detected format — e.g. d/m/Y]
- **Currency**: [detected format]
- **Numbers**: [decimal separator detected]

## Mandatory Rules
- [ ] No hardcoded text in templates or code
- [ ] Both languages complete before merge
- [ ] Descriptive variable names: {name}, {date}, {count}

## Multilingual SEO
[If hreflang config or other tags detected]
```

---

## .ai/DOCUMENTATION.md

```markdown
# Documentation Standards

## Inline Code Documentation
[Detected standard — e.g. PHPDoc, JSDoc, Google-style docstrings]

### Required for:
- [ ] Public methods
- [ ] Public class properties
- [ ] Non-obvious business logic

### Format detected:
[Real example extracted from code]

## README Standards
[What each module/package README should contain]

## Changelog
[Format detected — e.g. Keep a Changelog, conventional commits auto-generation]

## API Documentation
[Tool detected — e.g. Swagger/OpenAPI, Postman collections, manual]
```

---

## .ai/TOOLS.md

```markdown
# Project Tools & Configuration

## Development Commands

```bash
# Extracted from package.json scripts, composer.json scripts, or Makefile
[command]    # description
[command]    # description
```

## Required Local Tools
[Versions extracted from .tool-versions, .nvmrc, composer.json, go.mod]

| Tool | Version | Install |
|------|---------|---------|
| [name] | [version] | [how] |

## Docker Setup
[If docker-compose.yml exists — services, ports, volumes]

## CI/CD Pipeline
[Extracted from .github/workflows/ or equivalent]

| Stage | Trigger | What it does |
|-------|---------|-------------|
| [stage] | [trigger] | [action] |

## IDE / Editor Config
[Extracted from .editorconfig, .vscode/, recommended extensions]
```

---

## .ai/ROADMAP.md

```markdown
# Roadmap

> ℹ️ Pending manual completion — roadmap cannot be inferred from code alone.

## Current Version
[If detectable from package.json, composer.json, or CHANGELOG]

## Known Pending Work
[Extracted from TODO/FIXME/HACK comments found in code]

| Comment | File | Priority |
|---------|------|---------|
| [TODO text] | [path] | [inferred] |

## Planned Features
> ℹ️ To be completed manually by the team.

## Technical Debt
[Detected patterns that suggest refactoring needs]
```

---

## .ai/GLOSSARY.md

```markdown
# Domain Glossary

> Terms specific to this project's business domain.
> Agents must use these exact terms in code, comments, and documentation.

| Term | Definition | Used in |
|------|-----------|---------|
| [term found in code/comments] | [definition] | [module/file] |

> ℹ️ Expand this glossary with domain expert input.
```
