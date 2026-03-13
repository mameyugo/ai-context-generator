# Template: AGENT.md

File location: project root.
Purpose: single entry point for any AI agent working on this project.

---

```markdown
# [Project Name] — AI Agent Guide

## Purpose
[Concise system description — extract from existing README or package.json description]

## Tech Stack
- **Backend**: [detected — e.g. PHP 8.3+, Symfony 6.4]
- **Frontend**: [detected — e.g. Twig, Bootstrap 5.3, AdminLTE 3.2]
- **Database**: [detected — e.g. MariaDB 10.6, Doctrine ORM]
- **Testing**: [detected — e.g. PHPUnit 11, Behat 3.x]
- **DevOps**: [detected — e.g. Docker, GitHub Actions]

## Non-Negotiable Principles
- [Convention or principle detected in real code — e.g. PHP 8.3 strict typing]
- [Central architectural pattern — e.g. DDD with encapsulated modules]
- [Test policy — e.g. tests inside each module under Test/]
- [Critical security policy — e.g. prepared statements mandatory]
- [i18n — e.g. Spanish and Galician required from day 1]

## Documentation Structure
See `.ai/` for detailed instructions:

| Area | File |
|------|------|
| Architecture & modules | `.ai/ARCHITECTURE.md` |
| Code conventions | `.ai/CONVENTIONS.md` |
| Testing | `.ai/TESTING.md` |
| Deployment | `.ai/DEPLOYMENT.md` |
| UI design system | `.ai/DESIGN-SYSTEM.md` |
| Security | `.ai/SECURITY.md` |
| Database | `.ai/DATABASE.md` |
| Internationalization | `.ai/I18N.md` |
| Technical documentation | `.ai/DOCUMENTATION.md` |
| Tools | `.ai/TOOLS.md` |
| Architectural decisions | `.ai/DECISIONS/` |

## AI Tool Compatibility
- **GitHub Copilot**: `.github/copilot-instructions.md` + `.ai-docs/*.md`
- **Cursor / Antigravity**: `.cursorrules` or `.ai/*.md`
- **Gemini / Claude / others**: This `AGENT.md` as entry point

## What Agents Must NOT Do
- ❌ [Detected restriction — e.g. do not mix logic in Controllers]
- ❌ [Detected restriction — e.g. no raw SQL queries outside Repositories]
- ❌ [Detected restriction — e.g. do not ignore strict typing]
```
