# ai-context-generator

> Generate structured AI documentation for any software project — automatically, without assumptions.

**ai-context-generator** is a collection of meta-prompts that instruct any AI assistant (GitHub Copilot, Cursor, Gemini, Claude, etc.) to analyze your codebase and produce a complete, project-specific documentation structure optimized for AI-assisted development.

No boilerplate. No generic templates. Everything is derived from what actually exists in your project.

---

## How It Works

1. Copy the prompt for your language
2. Paste it into your AI assistant of choice
3. The AI analyzes your project and generates a full `AGENT.md` + `.ai/` folder structure

The generated documentation covers architecture, coding conventions, testing strategy, security policies, database guidelines, deployment, design system, i18n, and more — all tailored to your detected stack.

---

## Generated Structure

```
your-project/
├── AGENT.md                   # Global entry point for AI agents
└── .ai/
    ├── ARCHITECTURE.md        # Architecture, patterns, module structure
    ├── CONVENTIONS.md         # Code style, naming, commit conventions
    ├── TESTING.md             # Testing strategy, locations, commands
    ├── DEPLOYMENT.md          # Deployment, environments, CI/CD
    ├── DESIGN-SYSTEM.md       # UI components, design system
    ├── SECURITY.md            # Mandatory security policies
    ├── DATABASE.md            # Database guides, schemas, queries
    ├── I18N.md                # Internationalization and localization
    ├── DOCUMENTATION.md       # Internal documentation standards
    ├── TOOLS.md               # Project tools and configuration
    ├── ROADMAP.md             # Roadmap and upcoming features
    ├── GLOSSARY.md            # Business domain glossary
    └── DECISIONS/             # Architectural Decision Records (ADRs)
        └── [YYYY-MM-DD]-NNN-[title].md
```

---

## Compatible With

| Tool | How it reads the docs |
|------|-----------------------|
| GitHub Copilot | `.github/copilot-instructions.md` + `.ai/` |
| Cursor | `.cursorrules` or `.ai/` |
| Gemini / Claude / others | `AGENT.md` + `.ai/` |

---

## Available Languages

| Language | File |
|----------|------|
| 🇬🇧 English | [AI-DOCS-GENERATOR.md](./AI-DOCS-GENERATOR.md) |
| 🇪🇸 Spanish / Español | [AI-DOCS-GENERATOR-es.md](./AI-DOCS-GENERATOR-es.md) |
| 🇧🇷 Portuguese / Português | [AI-DOCS-GENERATOR-pt.md](./AI-DOCS-GENERATOR-pt.md) |

More languages coming soon. PRs welcome.

---

## Supported Stacks

The prompts include specific detection and generation logic for:

- **PHP**: Symfony, Laravel, custom frameworks — including `mameyugo/jsonq` JSON persistence
- **Node.js / TypeScript**: Express, Fastify, NestJS — monorepo support
- **Python**: FastAPI, Django, Flask
- **Go**, **Rust**, **Java / Spring Boot**
- **Frontend**: React, Vue, Angular, Svelte, Twig, Blade
- **Databases**: MariaDB, PostgreSQL, MongoDB, Redis, JSON files
- **DevOps**: Docker, GitHub Actions, and common deployment platforms

---

## Key Principles

- **No assumptions**: documentation is based solely on what exists in the codebase
- **Concrete over generic**: if PHPUnit 11 is detected, it says PHPUnit 11 — not "a testing framework"
- **Respects existing conventions**: adapts to the project's real patterns
- **Flags inconsistencies**: documents contradictions found in the code
- **Marks unknowns honestly**: uses `> ℹ️ Pending manual completion` instead of inventing content

---

## Contributing

Contributions are welcome — new languages, stack-specific improvements, or corrections to existing prompts.

1. Fork the repository
2. Create your branch: `git checkout -b feat/language-xx`
3. Add your file following the naming convention: `AI-DOCS-GENERATOR-xx.md`
4. Open a pull request

---

## License

MIT © [mameyugo](https://github.com/mameyugo)
