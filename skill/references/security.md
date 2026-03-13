# Template: .ai/SECURITY.md

---

```markdown
# Security Policies

> ⚠️ Always consult this file before implementing any feature that processes
> user input, handles authentication, or accesses data.

## Priority OWASP Vulnerabilities
[List based on detected application type]

## Mandatory Rules

### SQL / Database
[Detected rules — e.g. always prepared statements, never query with concatenation]

### Input Validation
[Detected policy — e.g. double validation client-side + server-side]

### Authentication & Sessions
[Detected mechanism — e.g. JWT, native PHP sessions, OAuth]

### Security Headers
[If detected config — nginx.conf, .htaccess, middleware]

### Sensitive Data
[Log policy, encryption of sensitive fields, GDPR if applicable]

## Pre-commit Security Checklist
- [ ] [Project-specific check]
- [ ] Input validated server-side
- [ ] No credentials in source code
- [ ] No concatenated SQL
```
