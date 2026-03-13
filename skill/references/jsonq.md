# JsonQ Detection & Integration Guide

## Detection Checklist

Run these checks before deciding whether to include the JsonQ section in DATABASE.md:

### 1. composer.json
```json
"require": {
    "mameyugo/jsonq": "*"
}
```
→ If present: **JsonQ confirmed**.

### 2. PHP extension
Look for `extension=jsonq.so` in:
- `php.ini`
- `conf.d/*.ini`
- Docker build scripts

### 3. Code usage
Search for these patterns in `.php` files:
```
JsonQ::open(
JsonQ::collection(
->from(
->where(
->insert(
->beginTransaction(
```

### 4. Data folders
Look for these directories with `*.json` files structured as collections
(arrays of objects, not config files):
- `data/`
- `storage/json/`
- `db/json/`
- `resources/data/`

### 5. Auto-generated indexes
An `indexes/` subfolder inside the data directory confirms JsonQ is actively used.

---

## Coexistence with Relational DB

If both MariaDB (or another RDBMS) and JsonQ are present, document clearly:

```markdown
### When to Use jsonq vs MariaDB

| Use case | Recommended engine |
|----------|--------------------|
| [detected use case] | jsonq / MariaDB |
```

Common split patterns to look for:
- JsonQ for config/settings, MariaDB for transactional data
- JsonQ for a specific isolated module, MariaDB for the rest
- JsonQ as the sole persistence layer (lightweight apps)

---

## ADR to Generate

When JsonQ is detected, always generate an ADR:

**File**: `.ai/DECISIONS/[YYYY-MM-DD]-NNN-json-file-persistence.md`

Key points to cover in the ADR:
- Why JSON files instead of a relational DB
- Trade-offs: simplicity/portability vs concurrent write limits
- Which modules use JsonQ and which use the RDBMS (if coexistence)
- Backup and deployment implications

---

## .gitignore Recommendations

Add to the project's `.gitignore` checklist:
```
# JsonQ auto-generated indexes (regenerated automatically)
data/indexes/

# JSON data files if they contain sensitive data
# (only if not used as fixtures/seeds)
# data/*.json
```
