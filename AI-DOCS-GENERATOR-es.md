# Generación Automática de Documentación para Agentes de IA — v2

Eres un agente de IA experto en análisis de código y documentación técnica. Tu tarea es analizar la base de código de este proyecto y generar una estructura completa de documentación para agentes de IA, siguiendo el estándar híbrido `AGENT.md` + carpeta `.ai/`, compatible con GitHub Copilot, Cursor y cualquier otro asistente.

---

## 🎯 Objetivo

Crear documentación estructurada que permita a cualquier agente de IA (GitHub Copilot, Cursor, Gemini, Claude) entender y trabajar efectivamente en el proyecto, **sin hacer suposiciones**: toda la documentación debe basarse en lo que realmente existe en la base de código.

---

## 📁 Estructura a Generar

```
proyecto/
├── AGENT.md                        # Punto de entrada global para agentes
└── .ai/
    ├── ARCHITECTURE.md             # Arquitectura, patrones y estructura de módulos
    ├── CONVENTIONS.md              # Convenciones de código, nombrado, commits
    ├── TESTING.md                  # Estrategia de testing, ubicación, comandos
    ├── DEPLOYMENT.md               # Despliegue, entornos, CI/CD
    ├── DESIGN-SYSTEM.md            # UI, componentes, sistema de diseño
    ├── SECURITY.md                 # Políticas de seguridad obligatorias
    ├── DATABASE.md                 # Guías de base de datos, esquemas, queries
    ├── I18N.md                     # Internacionalización y localización
    ├── DOCUMENTATION.md            # Estándares de documentación interna
    ├── TOOLS.md                    # Herramientas del proyecto y su configuración
    ├── ROADMAP.md                  # Hoja de ruta y próximas funcionalidades
    ├── GLOSSARY.md                 # Términos específicos del dominio de negocio
    └── DECISIONS/                  # Registro de decisiones arquitectónicas (ADRs)
        └── [YYYY-MM-DD]-NNN-[titulo].md
```

> **Nota sobre compatibilidad**: Si el proyecto ya tiene una carpeta `.ai-docs/`, genera también un `AGENT.md` en la raíz que la referencie. No renombres ni muevas los archivos existentes; en su lugar, crea los nuevos en `.ai/` y sincroniza el contenido donde corresponda.

---

## 🔍 Análisis Previo Obligatorio

**Antes de generar cualquier archivo**, realiza un análisis exhaustivo en tres fases.

### Fase 1: Detección del Stack Tecnológico

Examina los siguientes indicadores:

**Backend:**
- `composer.json` / `requirements.txt` / `go.mod` / `package.json` (dependencias)
- Extensiones predominantes en `src/` o `app/`: `.php`, `.py`, `.ts`, `.go`, `.java`
- Frameworks detectados: Symfony, Laravel, Django, FastAPI, Spring Boot, Express, etc.
- Versión del lenguaje en configuración: `composer.json` → `require.php`, `.nvmrc`, `go.mod`, etc.

**Frontend:**
- `package.json` devDependencies: React, Vue, Angular, Alpine.js, etc.
- Archivos de configuración: `vite.config.*`, `webpack.config.*`, `tailwind.config.*`
- Templates: `.twig`, `.blade.php`, `.html`, `.jsx`, `.vue`, `.svelte`
- Librerías CSS: Bootstrap, Tailwind, AdminLTE, Bulma

**Base de datos:**
- Archivos `*.sql`, `schema.sql`, `migrations/`
- ORM detectado: Doctrine, Eloquent, Prisma, SQLAlchemy, GORM
- Motor: `docker-compose.yml` (imagen mysql/mariadb/postgres/mongo), archivos `.env.example`
- **Persistencia en ficheros JSON**: presencia de `mameyugo/jsonq` en `composer.json` y/o carpetas `data/`, `storage/json/`, `db/json/` con archivos `*.json` estructurados como colecciones

**DevOps:**
- `Dockerfile`, `docker-compose.yml`
- `.github/workflows/*.yml` para CI/CD
- `Makefile`, `justfile`, scripts en `bin/` o `scripts/`
- Archivos de plataforma: `serverless.yml`, `render.yaml`, `fly.toml`, `.platform.app.yaml`

### Fase 2: Detección de Patrones Arquitectónicos

Mapea la estructura real de carpetas:

```
Patrones por estructura detectada:
- /Controllers, /Models, /Views               → MVC clásico
- /domain, /application, /infrastructure      → Clean Architecture / DDD
- /lib/Controllers, /lib/Services, /lib/Entities, /lib/Repositories, /lib/ValueObjects
                                              → DDD modular
- /components, /pages, /hooks                 → React/Next.js organizado
- /modulos/{nombreModulo}/lib/...             → Arquitectura de módulos encapsulados
- /Test/ dentro de cada módulo                → Tests encapsulados por módulo
- /data/*.json + mameyugo/jsonq en composer   → Persistencia en ficheros JSON con JsonQ
```

**Detección específica de mameyugo/jsonq:**
- `composer.json` contiene `"mameyugo/jsonq"` en `require` o `require-dev`
- Extensión PHP cargada: buscar `extension=jsonq.so` en `php.ini` o `conf.d/`
- Uso en código: buscar `JsonQ::open(`, `JsonQ::collection(`, `->where(`, `->insert(` en archivos `.php`
- Carpetas de datos: `data/`, `storage/json/`, `db/json/`, `resources/data/` con archivos `.json`
- Carpeta de índices: `data/indexes/` o similar (generada automáticamente por JsonQ)

Identifica también:
- Patrones de inyección de dependencias
- Value Objects con autovalidación
- Repositorios como abstracción de persistencia
- Servicios de aplicación vs servicios de dominio

### Fase 3: Detección de Convenciones Reales

Lee directamente los archivos de configuración presentes:
- `.editorconfig` → indentación, fin de línea
- `.prettierrc` / `.php-cs-fixer.php` / `.eslintrc` → estilo de código
- `.commitlintrc.json` / `commitlint.config.js` → formato de commits
- `phpstan.neon` / `.phpstan.neon` → nivel de análisis estático
- `.env.example` → variables de entorno reales

---

## 📝 Plantillas de los Archivos a Generar

### `AGENT.md` (raíz del proyecto)

```markdown
# [Nombre del Proyecto] — Guía para Agentes de IA

## Propósito
[Descripción concisa del sistema basada en README existente o package.json]

## Stack Tecnológico
- **Backend**: [detectado — ej: PHP 8.3+, Symfony 6.4]
- **Frontend**: [detectado — ej: Twig, Bootstrap 5.3, AdminLTE 3.2]
- **Base de Datos**: [detectado — ej: MariaDB 10.6, Doctrine ORM]
- **Testing**: [detectado — ej: PHPUnit 11, Behat 3.x]
- **DevOps**: [detectado — ej: Docker, GitHub Actions]

## Principios No Negociables
- [Convención o principio detectado en código real — ej: tipado estricto PHP 8.3]
- [Patrón arquitectónico central — ej: DDD con módulos encapsulados]
- [Política de tests — ej: tests dentro de cada módulo en Test/]
- [Política de seguridad crítica — ej: prepared statements obligatorios]
- [i18n — ej: español y gallego obligatorios desde el día 1]

## Estructura de la Documentación para Agentes
Consulta `.ai/` para instrucciones detalladas:

| Área | Archivo |
|------|---------|
| Arquitectura y módulos | `.ai/ARCHITECTURE.md` |
| Convenciones de código | `.ai/CONVENTIONS.md` |
| Testing | `.ai/TESTING.md` |
| Despliegue | `.ai/DEPLOYMENT.md` |
| Sistema de diseño UI | `.ai/DESIGN-SYSTEM.md` |
| Seguridad | `.ai/SECURITY.md` |
| Base de datos | `.ai/DATABASE.md` |
| Internacionalización | `.ai/I18N.md` |
| Documentación técnica | `.ai/DOCUMENTATION.md` |
| Herramientas | `.ai/TOOLS.md` |
| Decisiones arquitectónicas | `.ai/DECISIONS/` |

## Compatibilidad con Herramientas de IA
- **GitHub Copilot**: Lee `.github/copilot-instructions.md` + `.ai-docs/*.md`
- **Cursor / Antigravity**: Lee `.cursorrules` o archivos en `.ai/`
- **Gemini / Claude / otros**: Lee este `AGENT.md` como punto de entrada

## Lo que los Agentes NO Deben Hacer
- ❌ [Restricción detectada en el proyecto — ej: no mezclar lógica en Controllers]
- ❌ [Restricción detectada — ej: no queries SQL directas fuera de Repositories]
- ❌ [Restricción detectada — ej: no ignorar tipado estricto]
```

---

### `.ai/ARCHITECTURE.md`

```markdown
# Arquitectura del Proyecto

## Patrón Principal
[Descripción del patrón detectado, con justificación extraída del código real]

## Estructura de Módulos

[Árbol de directorios real del proyecto — usa `find` o `tree` para generarlo]

## Capas y Responsabilidades

| Capa | Ubicación | Responsabilidad |
|------|-----------|-----------------|
| [Capa detectada] | [ruta real] | [responsabilidad] |

## Reglas de Dependencia entre Capas
- [Capa A] puede depender de [Capa B]
- [Capa X] NO debe conocer [Capa Y]
- [Regla específica detectada en el código]

## Módulos Existentes
[Lista de módulos reales encontrados en app/modulos/ o src/]

| Módulo | Propósito | Dependencias conocidas |
|--------|-----------|----------------------|
| [nombre] | [descripción] | [deps] |

## Decisiones Arquitectónicas Clave
[Ver `.ai/DECISIONS/` para el registro completo]

## Integraciones Externas
[APIs, servicios de terceros, webhooks detectados en el código]
```

---

### `.ai/TESTING.md`

```markdown
# Estrategia de Testing

## Frameworks Detectados
- **Unitarios**: [ej: PHPUnit 11]
- **BDD/Integración**: [ej: Behat 3.x con escenarios en español]
- **E2E**: [si existe: Playwright, Cypress, Panther]
- **Análisis estático**: [ej: PHPStan nivel 8]

## Ubicación de Tests — REGLA CRÍTICA
[Describe la política real detectada. Ejemplo si se detecta encapsulación por módulo:]

Los tests están encapsulados dentro de cada módulo, NO en carpetas centrales:

✅ Correcto:
```
app/modulos/{nombreModulo}/Test/
├── Integration/
│   └── NombreModuloApiTest.php
└── Unitaries/
    └── NombreServicioTest.php
```

❌ Incorrecto:
```
Tests/Integration/  ← No usar
tests/unitaries/    ← No usar
```

Namespace correcto:
```php
namespace app\modulos\{nombreModulo}\Test\Integration;
namespace app\modulos\{nombreModulo}\Test\Unitaries;
```

## Comandos Detectados

```bash
# Extraído de composer.json scripts o Makefile
[comando real detectado]    # descripción
[comando real detectado]    # descripción
```

## Patrones de Testing
- **Mocks**: [cómo se usan en el proyecto]
- **Fixtures**: [ubicación y formato real]
- **Factories**: [si existen]
- **Setup/Teardown**: [hooks detectados]

## Cobertura Mínima Requerida
[Si está configurada — extraer de phpunit.xml o jest.config]

## Escenarios BDD (si aplica)
[Lenguaje y convención detectada — ej: Gherkin en español]
```

---

### `.ai/SECURITY.md`

```markdown
# Políticas de Seguridad

> ⚠️ Este archivo debe consultarse SIEMPRE antes de implementar cualquier funcionalidad
> que procese input de usuario, gestione autenticación o acceda a datos.

## Vulnerabilidades OWASP Prioritarias
[Lista basada en el tipo de aplicación detectada]

## Reglas Obligatorias

### SQL / Base de Datos
[Reglas detectadas — ej: siempre prepared statements, nunca query con concatenación]

### Validación de Input
[Política detectada — ej: validación doble client-side + server-side]

### Autenticación y Sesiones
[Mecanismo detectado — ej: JWT, sesiones PHP nativas, OAuth]

### Headers de Seguridad
[Si hay configuración detectada — nginx.conf, .htaccess, middleware]

### Datos Sensibles
[Política de logs, encriptación de campos sensibles, GDPR si aplica]

## Checklist Pre-commit de Seguridad
- [ ] [Verificación específica del proyecto]
- [ ] Input validado server-side
- [ ] Sin credenciales en código fuente
- [ ] Sin SQL concatenado
```

---

### `.ai/DATABASE.md`

```markdown
# Guías de Base de Datos

## Motor y Versión
[Detectado — ej: MariaDB 10.6]

## ORM / Abstracción
[Detectado — ej: Doctrine DBAL / custom Repositories]

## Convenciones de Esquema
[Extraídas de los archivos schema.sql o migraciones reales]

Ejemplo si se detecta el patrón de COMMENTs en MariaDB:
- Todos los campos deben tener COMMENT con formato `Descripción|validaciones`
- Ejemplo: `COMMENT 'Importe del pago|required;decimal;min:0'`

## Migraciones
[Herramienta y proceso detectado — ej: Phinx, Doctrine Migrations, SQL manual]

## Patrones de Query
[Extraer ejemplos reales del código — prepared statements, transacciones, etc.]

## Índices — Política
[Política detectada]

## Tablas Principales del Dominio
[Lista de tablas encontradas en schema.sql con su propósito]

| Tabla | Propósito |
|-------|-----------|
| [nombre real] | [descripción] |
```

---

### `.ai/I18N.md`

```markdown
# Internacionalización

## Idiomas Soportados
[Detectados — ej: español (es) y gallego (gl)]

## Sistema de Traducciones
[Detectado — ej: archivos YAML en /locales, función lang(), sistema Symfony Translator]

## Estructura de Archivos de Traducción
[Árbol real detectado]

## Convenciones de Claves
[Patrón detectado — ej: módulo.entidad.campo o módulo.accion.descripcion]

## Formatos Regionales
- **Fechas**: [formato detectado — ej: d/m/Y]
- **Moneda**: [formato detectado]
- **Números**: [separador decimal detectado]

## Reglas Obligatorias
- [ ] Ningún texto hardcodeado en templates o código
- [ ] Ambos idiomas completos antes de merge
- [ ] Variables con nombres descriptivos: {nombre}, {fecha}, {count}

## SEO Multilingüe
[Si hay configuración de hreflang u otras etiquetas detectadas]
```

---

### `.ai/DATABASE.md` — Variante con mameyugo/jsonq

Si se detecta `mameyugo/jsonq` como capa de persistencia (total o parcial), sustituye o complementa la plantilla genérica de DATABASE.md con:

```markdown
# Guías de Base de Datos

## Motor(es) de Persistencia Detectados

| Motor | Uso | Ubicación de datos |
|-------|-----|--------------------|
| [MariaDB / jsonq / ambos] | [toda la app / módulo X] | [ruta real] |

---

## mameyugo/jsonq — Motor de Persistencia JSON

### Qué es
Extensión PHP escrita en Rust que proporciona almacenamiento en ficheros `.json` con
queries estilo MongoDB, indexación, validación de esquema y transacciones ACID.
Requiere la extensión nativa `jsonq.so` cargada en PHP.

### Requisitos
- PHP >= 8.1
- Extensión `ext-jsonq` instalada (`php -m | grep jsonq`)
- Carpeta de datos con permisos de escritura para PHP

### Estructura de Datos Detectada

```
[ruta raíz de datos — ej: data/]
├── [coleccion1].json          # Equivale a una tabla/colección
├── [coleccion2].json
├── indexes/                   # Índices autogenerados por JsonQ — NO editar
│   ├── [coleccion1]/
│   └── [coleccion2]/
└── schemas/                   # Esquemas de validación (si existen)
    └── [coleccion1].schema.json
```

### Colecciones Existentes

| Colección (fichero .json) | Propósito | Campos principales detectados |
|--------------------------|-----------|-------------------------------|
| [nombre real] | [descripción] | [campos inferidos del JSON] |

### Patrón de Acceso en el Proyecto

```php
// Patrón detectado en Repositories — ajustar según el código real

// Lectura con query
$resultado = JsonQ::open('data/[coleccion].json')
    ->from('[coleccion]')
    ->where('campo', '=', $valor)
    ->get();

// Inserción
JsonQ::open('data/[coleccion].json')
    ->insert(['campo' => $valor, ...]);

// Actualización
JsonQ::open('data/[coleccion].json')
    ->from('[coleccion]')
    ->where('id', '=', $id)
    ->update(['campo' => $nuevoValor]);

// Eliminación
JsonQ::open('data/[coleccion].json')
    ->from('[coleccion]')
    ->where('id', '=', $id)
    ->delete();

// Transacción ACID (si el proyecto las usa)
$db = JsonQ::open('data/[coleccion].json');
$db->beginTransaction();
try {
    $db->insert([...]);
    $db->commit();
} catch (\Exception $e) {
    $db->rollback();
    throw $e;
}
```

### Reglas Obligatorias del Proyecto

- [ ] **Nunca editar los `.json` de datos directamente** — usar siempre la API de JsonQ
- [ ] **Nunca editar la carpeta `indexes/`** — es autogestionada por JsonQ
- [ ] **IDs**: [describir la política de IDs detectada — UUID, autoincremento manual, etc.]
- [ ] **Validación**: realizar siempre en el Service/ValueObject antes de persistir,
      JsonQ no valida tipos por defecto salvo que se configure un schema
- [ ] **Concurrencia**: JsonQ usa file locking — documentar si hay procesos concurrentes
- [ ] **Backups**: los ficheros `.json` son la fuente de verdad — incluir en política de backup

### Cuándo Usar jsonq vs [otra BD si coexiste]

> ⚠️ Si el proyecto usa tanto MariaDB como jsonq, documentar aquí qué módulos
> usan cada motor y la razón de la coexistencia.

| Escenario | Motor recomendado |
|-----------|------------------|
| [caso de uso del proyecto] | jsonq / MariaDB |

### Rendimiento

- JsonQ usa SIMD parsing (simd-json) y caché Arc con invalidación por mtime
- Los índices hash permiten lookups O(1) en campos indexados
- Para colecciones grandes (>10k registros), verificar si hay índices definidos
- El file locking puede ser cuello de botella con alta concurrencia

### Checklist de Diseño con jsonq

- [ ] Carpeta de datos fuera del directorio público (`public/`, `web/`)
- [ ] Permisos correctos en carpeta de datos (escritura solo para PHP, no acceso web)
- [ ] Colecciones con esquema de validación definido si jsonq lo soporta
- [ ] Política de IDs consistente en todo el proyecto
- [ ] Carpeta `indexes/` en `.gitignore` o equivalente (se regenera automáticamente)
- [ ] Ficheros `.json` de datos en `.gitignore` si contienen datos sensibles
- [ ] Backups automatizados de los ficheros `.json`
```

---

### `.ai/DECISIONS/[YYYY-MM-DD]-NNN-[titulo].md`

Para cada decisión arquitectónica importante detectada en el código, genera un ADR:

```markdown
# [NNN]: [Título de la Decisión]

**Fecha**: [YYYY-MM-DD]
**Estado**: Aceptada | Propuesta | Reemplazada por NNN

## Contexto
[Qué problema o necesidad motivó esta decisión — inferido del código]

## Decisión
[Qué se decidió implementar]

## Consecuencias

**Positivas:**
- [consecuencia]

**Negativas / Trade-offs:**
- [consecuencia]

## Alternativas Descartadas
1. **[Alternativa]**: [por qué no se eligió]

## Archivos Relacionados
- [Rutas reales en el proyecto]
```

---

## 🔧 Instrucciones Específicas por Stack

### Si detectas PHP + Symfony/Custom Framework

- Analiza `composer.json` para versión de PHP y dependencias
- Mapea la estructura de módulos en `app/modulos/` o `src/`
- Detecta el patrón de Controllers (thin vs fat), Services y Repositories
- Identifica si se usan Value Objects con autovalidación
- Comprueba si `phpstan.neon` existe y extrae el nivel configurado
- Extrae comandos de `composer.json` → `scripts`
- Detecta el sistema de traducciones (Symfony Translator, custom `lang()`, etc.)
- Documenta la política de COMMENT en campos de BD si existe en los `.sql`

**Si además se detecta `mameyugo/jsonq`** (puede coexistir con MariaDB o ser la única persistencia):
- Verifica si `extension=jsonq.so` está habilitada en la configuración PHP
- Identifica la carpeta raíz de datos JSON (habitualmente `data/` o `storage/json/`)
- Lista los archivos `.json` existentes — cada uno equivale a una "colección/tabla"
- Detecta si hay carpeta `indexes/` autogenerada (indica indexación activa)
- Busca el patrón de acceso en Repositories: `JsonQ::open('ruta/coleccion.json')`
- Determina si jsonq se usa para **toda** la persistencia o solo en módulos específicos
- Documenta los esquemas JSON implícitos leyendo la estructura de los archivos de datos
- Identifica si se usan transacciones JsonQ (`->beginTransaction()`, `->commit()`, `->rollback()`)
- Genera `.ai/DATABASE.md` con la sección JsonQ según la plantilla específica más abajo

### Si detectas Node.js / TypeScript

- Analiza `package.json` dependencies y scripts
- Mapea si es Express, Fastify, NestJS u otro
- Detecta si hay `tsconfig.json` y extrae `strict`, `target`, `paths`
- Comprueba `jest.config.*` o `vitest.config.*`
- Identifica si hay monorepo (Turborepo, Nx, workspaces)

### Si detectas Python

- Analiza `requirements.txt`, `pyproject.toml` o `Pipfile`
- Detecta framework: FastAPI, Django, Flask
- Comprueba `mypy.ini` o `pyproject.toml` [mypy] para tipos
- Extrae configuración de pytest

### Si detectas múltiples stacks (monorepo)

- Documenta cada uno por separado en secciones de ARCHITECTURE.md
- Identifica las fronteras de comunicación entre stacks
- Genera ADR específico sobre la decisión de monorepo

---

## 🔗 Integración con Documentación Existente

Si encuentras archivos de documentación preexistentes, **no los elimines**. En cambio:

| Encontrado | Acción |
|------------|--------|
| `.ai-docs/*.md` | Referencia desde `.ai/*.md` y sincroniza contenido |
| `.github/copilot-instructions.md` | Mantén y añade referencia a `.ai/` |
| `.cursorrules` | Mantén y añade referencia a `.ai/` |
| `CLAUDE.md` | Mantén y añade referencia a `.ai/` |
| `README.md` | Extrae información técnica para `AGENT.md` |

En `AGENT.md`, documenta qué archivos existen para cada herramienta:

```markdown
## Compatibilidad con Herramientas de IA
- **GitHub Copilot**: `.github/copilot-instructions.md` + `.ai-docs/*.md`
- **Cursor**: `.cursorrules` o `.ai/*.md`
- **Gemini / Claude**: Este `AGENT.md` + `.ai/*.md`
```

---

## 📊 Resumen de Salida Esperada

Al finalizar el análisis, proporciona un resumen estructurado:

```markdown
## ✅ Documentación Generada

### Stack Detectado
- **Lenguaje principal**: [...]
- **Framework**: [...]
- **BD / Persistencia**: [...] *(si se detecta jsonq: "mameyugo/jsonq — ficheros JSON" o "MariaDB + mameyugo/jsonq")*
- **Testing**: [...]
- **DevOps**: [...]

### Archivos Generados
- [x] `AGENT.md`
- [x] `.ai/ARCHITECTURE.md`
- [x] `.ai/CONVENTIONS.md`
- [x] `.ai/TESTING.md`
- [x] `.ai/SECURITY.md`
- [x] `.ai/DATABASE.md`
- [x] `.ai/DESIGN-SYSTEM.md`
- [x] `.ai/I18N.md`
- [x] `.ai/DOCUMENTATION.md`
- [x] `.ai/TOOLS.md`
- [x] `.ai/ROADMAP.md`
- [x] `.ai/GLOSSARY.md`

### ADRs Generados
- [x] `.ai/DECISIONS/[fecha]-001-[decision].md`
- [x] `.ai/DECISIONS/[fecha]-002-[decision].md`
*(Si se detecta jsonq: generar ADR específico sobre la decisión de usar persistencia en ficheros JSON y sus trade-offs frente a una BD relacional)*

### Documentación Preexistente Detectada
| Archivo | Estado |
|---------|--------|
| `.ai-docs/*.md` | Referenciado desde `.ai/` |
| `.github/copilot-instructions.md` | Mantenido, referencia añadida |

### ⚠️ Áreas sin Información Suficiente
- [ ] **[Área]**: [qué falta y recomendación]
- [ ] **[Área]**: [qué falta y recomendación]

### 🔍 Inconsistencias Detectadas
- **[Inconsistencia]**: [descripción y recomendación]

## 🚀 Próximos Pasos Recomendados
1. Revisar y ajustar los archivos generados
2. Completar las secciones marcadas como incompletas
3. Crear el primer ADR para la decisión más importante del proyecto
4. Compartir con el equipo para validación
5. Actualizar la documentación con cada cambio arquitectónico significativo
```

---

## 🎯 Comportamiento Esperado del Agente

- **No modificar código existente**: solo lectura, nunca escritura en archivos fuente
- **Específico, no genérico**: si encuentras que se usa PHPUnit, no escribas "framework de testing"; escribe "PHPUnit 11"
- **Documentar suposiciones**: si algo no está claro en el código, indícalo explícitamente en el archivo generado con `> ⚠️ Suposición: ...`
- **Señalar inconsistencias**: si encuentras patrones contradictorios (ej: algunos módulos con tests encapsulados y otros no), documéntalo
- **Priorizar lo crítico**: genera primero AGENT.md, ARCHITECTURE.md y SECURITY.md; el resto puede generarse iterativamente

---

## 🚀 Comienza el Análisis

Analiza el proyecto actual siguiendo las tres fases descritas y genera la documentación en el orden recomendado. Si alguna sección no tiene información suficiente en el código, déjala con una nota `> ℹ️ Pendiente de completar manualmente` en lugar de inventar contenido.
