# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [Unreleased]

---

## [2.0.0] - 2026-03-12

### Added
- Complete rewrite of the prompt with a structured three-phase analysis framework
- Phase 1: Technology stack detection (backend, frontend, database, DevOps)
- Phase 2: Architectural pattern detection (MVC, DDD, Clean Architecture, modular)
- Phase 3: Real convention detection from config files (`.editorconfig`, `.prettierrc`, `phpstan.neon`, etc.)
- Full `.ai/` folder structure: 12 specialized documentation files + ADR registry
- `AGENT.md` root entry point compatible with GitHub Copilot, Cursor, Gemini, Claude, and others
- Specific detection and documentation support for `mameyugo/jsonq` JSON persistence engine
- Stack-specific instructions for PHP/Symfony, Node.js/TypeScript, Python, Go, Rust
- ADR (Architectural Decision Record) template and auto-generation logic
- Integration guide for pre-existing documentation (`.ai-docs/`, `.cursorrules`, `CLAUDE.md`)
- Structured output summary with inconsistency and coverage gap reporting
- Spanish version (`AI-DOCS-GENERATOR-es.md`)
- English version (`AI-DOCS-GENERATOR.md`)
- Portuguese/Brazilian version (`AI-DOCS-GENERATOR-pt.md`)

### Changed
- Prompt structure reorganized from flat instructions to a phased analysis approach
- Documentation output expanded from 7 to 12 specialized files
- Security policy template now includes OWASP priorities tailored to the detected app type
- Database template now covers both relational and JSON file persistence patterns
- Agent behavior guidelines made more explicit: specific over generic, flag inconsistencies, mark unknowns

### Removed
- Generic boilerplate examples not tied to real code detection

---

## [1.0.0] - 2026-01-29

### Added
- Initial release of the AI documentation meta-prompt
- Seven specialized documentation types: copilot instructions, architecture guidelines, design system, security policies, testing strategies, database guidelines, internationalization guides
- Support for Python/FastAPI, Java/Spring Boot, Node.js/Express, Go/Gin, Rust/Actix-web
- Basic stack detection logic
- `.ai-docs/` folder structure as output target
- Spanish-only prompt

[Unreleased]: https://github.com/mameyugo/ai-context-generator/compare/v2.0.0...HEAD
[2.0.0]: https://github.com/mameyugo/ai-context-generator/compare/v1.0.0...v2.0.0
[1.0.0]: https://github.com/mameyugo/ai-context-generator/releases/tag/v1.0.0
