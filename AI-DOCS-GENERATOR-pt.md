# Geração Automática de Documentação para Agentes de IA — v2

Você é um agente de IA especialista em análise de código e documentação técnica. Sua tarefa é analisar a base de código deste projeto e gerar uma estrutura completa de documentação para agentes de IA, seguindo o padrão híbrido `AGENT.md` + pasta `.ai/`, compatível com GitHub Copilot, Cursor e qualquer outro assistente.

---

## 🎯 Objetivo

Criar documentação estruturada que permita a qualquer agente de IA (GitHub Copilot, Cursor, Gemini, Claude) entender e trabalhar efetivamente no projeto, **sem fazer suposições**: toda a documentação deve ser baseada no que realmente existe na base de código.

---

## 📁 Estrutura a Gerar

```
projeto/
├── AGENT.md                        # Ponto de entrada global para agentes
└── .ai/
    ├── ARCHITECTURE.md             # Arquitetura, padrões e estrutura de módulos
    ├── CONVENTIONS.md              # Convenções de código, nomenclatura, commits
    ├── TESTING.md                  # Estratégia de testes, localização, comandos
    ├── DEPLOYMENT.md               # Deploy, ambientes, CI/CD
    ├── DESIGN-SYSTEM.md            # UI, componentes, sistema de design
    ├── SECURITY.md                 # Políticas de segurança obrigatórias
    ├── DATABASE.md                 # Guias de banco de dados, esquemas, queries
    ├── I18N.md                     # Internacionalização e localização
    ├── DOCUMENTATION.md            # Padrões de documentação interna
    ├── TOOLS.md                    # Ferramentas do projeto e sua configuração
    ├── ROADMAP.md                  # Roadmap e próximas funcionalidades
    ├── GLOSSARY.md                 # Termos específicos do domínio de negócio
    └── DECISIONS/                  # Registro de decisões arquiteturais (ADRs)
        └── [YYYY-MM-DD]-NNN-[titulo].md
```

> **Nota de compatibilidade**: Se o projeto já possui uma pasta `.ai-docs/`, gere também um `AGENT.md` na raiz que a referencie. Não renomeie nem mova arquivos existentes; em vez disso, crie os novos em `.ai/` e sincronize o conteúdo onde for apropriado.

---

## 🔍 Análise Prévia Obrigatória

**Antes de gerar qualquer arquivo**, realize uma análise completa em três fases.

### Fase 1: Detecção do Stack Tecnológico

Examine os seguintes indicadores:

**Backend:**
- `composer.json` / `requirements.txt` / `go.mod` / `package.json` (dependências)
- Extensões predominantes em `src/` ou `app/`: `.php`, `.py`, `.ts`, `.go`, `.java`
- Frameworks detectados: Symfony, Laravel, Django, FastAPI, Spring Boot, Express, etc.
- Versão da linguagem na configuração: `composer.json` → `require.php`, `.nvmrc`, `go.mod`, etc.

**Frontend:**
- `package.json` devDependencies: React, Vue, Angular, Alpine.js, etc.
- Arquivos de configuração: `vite.config.*`, `webpack.config.*`, `tailwind.config.*`
- Templates: `.twig`, `.blade.php`, `.html`, `.jsx`, `.vue`, `.svelte`
- Bibliotecas CSS: Bootstrap, Tailwind, AdminLTE, Bulma

**Banco de Dados:**
- Arquivos `*.sql`, `schema.sql`, `migrations/`
- ORM detectado: Doctrine, Eloquent, Prisma, SQLAlchemy, GORM
- Motor: `docker-compose.yml` (imagem mysql/mariadb/postgres/mongo), arquivos `.env.example`
- **Persistência em arquivos JSON**: presença de `mameyugo/jsonq` em `composer.json` e/ou pastas `data/`, `storage/json/`, `db/json/` com arquivos `*.json` estruturados como coleções

**DevOps:**
- `Dockerfile`, `docker-compose.yml`
- `.github/workflows/*.yml` para CI/CD
- `Makefile`, `justfile`, scripts em `bin/` ou `scripts/`
- Arquivos de plataforma: `serverless.yml`, `render.yaml`, `fly.toml`, `.platform.app.yaml`

### Fase 2: Detecção de Padrões Arquiteturais

Mapeie a estrutura real de pastas:

```
Padrões por estrutura detectada:
- /Controllers, /Models, /Views               → MVC clássico
- /domain, /application, /infrastructure      → Clean Architecture / DDD
- /lib/Controllers, /lib/Services, /lib/Entities, /lib/Repositories, /lib/ValueObjects
                                              → DDD modular
- /components, /pages, /hooks                 → React/Next.js organizado
- /modulos/{nomeModulo}/lib/...               → Arquitetura de módulos encapsulados
- /Test/ dentro de cada módulo                → Testes encapsulados por módulo
- /data/*.json + mameyugo/jsonq no composer   → Persistência em arquivos JSON com JsonQ
```

**Detecção específica de mameyugo/jsonq:**
- `composer.json` contém `"mameyugo/jsonq"` em `require` ou `require-dev`
- Extensão PHP carregada: buscar `extension=jsonq.so` em `php.ini` ou `conf.d/`
- Uso no código: buscar `JsonQ::open(`, `JsonQ::collection(`, `->where(`, `->insert(` em arquivos `.php`
- Pastas de dados: `data/`, `storage/json/`, `db/json/`, `resources/data/` com arquivos `.json`
- Pasta de índices: `data/indexes/` ou similar (gerada automaticamente pelo JsonQ)

Identifique também:
- Padrões de injeção de dependência
- Value Objects com autovalidação
- Repositórios como abstração de persistência
- Serviços de aplicação vs serviços de domínio

### Fase 3: Detecção de Convenções Reais

Leia diretamente os arquivos de configuração presentes:
- `.editorconfig` → indentação, fim de linha
- `.prettierrc` / `.php-cs-fixer.php` / `.eslintrc` → estilo de código
- `.commitlintrc.json` / `commitlint.config.js` → formato de commits
- `phpstan.neon` / `.phpstan.neon` → nível de análise estática
- `.env.example` → variáveis de ambiente reais

---

## 📝 Templates dos Arquivos a Gerar

### `AGENT.md` (raiz do projeto)

```markdown
# [Nome do Projeto] — Guia para Agentes de IA

## Propósito
[Descrição concisa do sistema baseada no README existente ou package.json]

## Stack Tecnológico
- **Backend**: [detectado — ex: PHP 8.3+, Symfony 6.4]
- **Frontend**: [detectado — ex: Twig, Bootstrap 5.3, AdminLTE 3.2]
- **Banco de Dados**: [detectado — ex: MariaDB 10.6, Doctrine ORM]
- **Testes**: [detectado — ex: PHPUnit 11, Behat 3.x]
- **DevOps**: [detectado — ex: Docker, GitHub Actions]

## Princípios Não Negociáveis
- [Convenção ou princípio detectado no código real — ex: tipagem estrita PHP 8.3]
- [Padrão arquitetural central — ex: DDD com módulos encapsulados]
- [Política de testes — ex: testes dentro de cada módulo em Test/]
- [Política de segurança crítica — ex: prepared statements obrigatórios]
- [i18n — ex: português e inglês obrigatórios desde o dia 1]

## Estrutura da Documentação para Agentes
Consulte `.ai/` para instruções detalhadas:

| Área | Arquivo |
|------|---------|
| Arquitetura e módulos | `.ai/ARCHITECTURE.md` |
| Convenções de código | `.ai/CONVENTIONS.md` |
| Testes | `.ai/TESTING.md` |
| Deploy | `.ai/DEPLOYMENT.md` |
| Sistema de design UI | `.ai/DESIGN-SYSTEM.md` |
| Segurança | `.ai/SECURITY.md` |
| Banco de dados | `.ai/DATABASE.md` |
| Internacionalização | `.ai/I18N.md` |
| Documentação técnica | `.ai/DOCUMENTATION.md` |
| Ferramentas | `.ai/TOOLS.md` |
| Decisões arquiteturais | `.ai/DECISIONS/` |

## Compatibilidade com Ferramentas de IA
- **GitHub Copilot**: Lê `.github/copilot-instructions.md` + `.ai-docs/*.md`
- **Cursor / Antigravity**: Lê `.cursorrules` ou arquivos em `.ai/`
- **Gemini / Claude / outros**: Lê este `AGENT.md` como ponto de entrada

## O que os Agentes NÃO Devem Fazer
- ❌ [Restrição detectada no projeto — ex: não misturar lógica nos Controllers]
- ❌ [Restrição detectada — ex: sem queries SQL diretas fora dos Repositories]
- ❌ [Restrição detectada — ex: não ignorar tipagem estrita]
```

---

### `.ai/ARCHITECTURE.md`

```markdown
# Arquitetura do Projeto

## Padrão Principal
[Descrição do padrão detectado, com justificativa extraída do código real]

## Estrutura de Módulos

[Árvore de diretórios real do projeto — use `find` ou `tree` para gerar]

## Camadas e Responsabilidades

| Camada | Localização | Responsabilidade |
|--------|-------------|-----------------|
| [Camada detectada] | [caminho real] | [responsabilidade] |

## Regras de Dependência entre Camadas
- [Camada A] pode depender de [Camada B]
- [Camada X] NÃO deve conhecer [Camada Y]
- [Regra específica detectada no código]

## Módulos Existentes
[Lista de módulos reais encontrados em app/modulos/ ou src/]

| Módulo | Propósito | Dependências conhecidas |
|--------|-----------|------------------------|
| [nome] | [descrição] | [deps] |

## Decisões Arquiteturais Chave
[Veja `.ai/DECISIONS/` para o registro completo]

## Integrações Externas
[APIs, serviços de terceiros, webhooks detectados no código]
```

---

### `.ai/TESTING.md`

```markdown
# Estratégia de Testes

## Frameworks Detectados
- **Unitários**: [ex: PHPUnit 11]
- **BDD/Integração**: [ex: Behat 3.x com cenários em português]
- **E2E**: [se existir: Playwright, Cypress, Panther]
- **Análise estática**: [ex: PHPStan nível 8]

## Localização dos Testes — REGRA CRÍTICA
[Descreva a política real detectada. Exemplo se encapsulamento por módulo for detectado:]

Os testes são encapsulados dentro de cada módulo, NÃO em pastas centrais:

✅ Correto:
```
app/modulos/{nomeModulo}/Test/
├── Integration/
│   └── NomeModuloApiTest.php
└── Unitaries/
    └── NomeServicoTest.php
```

❌ Incorreto:
```
Tests/Integration/  ← Não usar
tests/unitaries/    ← Não usar
```

Namespace correto:
```php
namespace app\modulos\{nomeModulo}\Test\Integration;
namespace app\modulos\{nomeModulo}\Test\Unitaries;
```

## Comandos Detectados

```bash
# Extraído de composer.json scripts ou Makefile
[comando real detectado]    # descrição
[comando real detectado]    # descrição
```

## Padrões de Teste
- **Mocks**: [como são usados no projeto]
- **Fixtures**: [localização e formato real]
- **Factories**: [se existirem]
- **Setup/Teardown**: [hooks detectados]

## Cobertura Mínima Exigida
[Se configurada — extrair de phpunit.xml ou jest.config]

## Cenários BDD (se aplicável)
[Linguagem e convenção detectada — ex: Gherkin em português]
```

---

### `.ai/SECURITY.md`

```markdown
# Políticas de Segurança

> ⚠️ Este arquivo deve ser consultado SEMPRE antes de implementar qualquer
> funcionalidade que processe input do usuário, gerencie autenticação ou acesse dados.

## Vulnerabilidades OWASP Prioritárias
[Lista baseada no tipo de aplicação detectada]

## Regras Obrigatórias

### SQL / Banco de Dados
[Regras detectadas — ex: sempre prepared statements, nunca query com concatenação]

### Validação de Input
[Política detectada — ex: validação dupla client-side + server-side]

### Autenticação e Sessões
[Mecanismo detectado — ex: JWT, sessões PHP nativas, OAuth]

### Headers de Segurança
[Se houver configuração detectada — nginx.conf, .htaccess, middleware]

### Dados Sensíveis
[Política de logs, criptografia de campos sensíveis, LGPD se aplicável]

## Checklist de Segurança Pré-commit
- [ ] [Verificação específica do projeto]
- [ ] Input validado no server-side
- [ ] Sem credenciais no código-fonte
- [ ] Sem SQL concatenado
```

---

### `.ai/DATABASE.md`

```markdown
# Guias de Banco de Dados

## Motor e Versão
[Detectado — ex: MariaDB 10.6]

## ORM / Abstração
[Detectado — ex: Doctrine DBAL / Repositories customizados]

## Convenções de Esquema
[Extraídas dos arquivos schema.sql ou migrações reais]

Exemplo se o padrão de COMMENTs no MariaDB for detectado:
- Todos os campos devem ter COMMENT com formato `Descrição|validações`
- Exemplo: `COMMENT 'Valor do pagamento|required;decimal;min:0'`

## Migrações
[Ferramenta e processo detectado — ex: Phinx, Doctrine Migrations, SQL manual]

## Padrões de Query
[Extrair exemplos reais do código — prepared statements, transações, etc.]

## Índices — Política
[Política detectada]

## Tabelas Principais do Domínio
[Lista de tabelas encontradas em schema.sql com seu propósito]

| Tabela | Propósito |
|--------|-----------|
| [nome real] | [descrição] |
```

---

### `.ai/I18N.md`

```markdown
# Internacionalização

## Idiomas Suportados
[Detectados — ex: português (pt-BR) e inglês (en)]

## Sistema de Traduções
[Detectado — ex: arquivos YAML em /locales, função lang(), Symfony Translator]

## Estrutura de Arquivos de Tradução
[Árvore real detectada]

## Convenções de Chaves
[Padrão detectado — ex: modulo.entidade.campo ou modulo.acao.descricao]

## Formatos Regionais
- **Datas**: [formato detectado — ex: dd/MM/yyyy]
- **Moeda**: [formato detectado — ex: R$ 1.234,56]
- **Números**: [separador decimal detectado — ex: vírgula]

## Regras Obrigatórias
- [ ] Nenhum texto hardcoded em templates ou código
- [ ] Ambos os idiomas completos antes do merge
- [ ] Variáveis com nomes descritivos: {nome}, {data}, {count}

## SEO Multilíngue
[Se houver configuração de hreflang ou outras tags detectadas]
```

---

### `.ai/DATABASE.md` — Variante com mameyugo/jsonq

Se `mameyugo/jsonq` for detectado como camada de persistência (total ou parcial), substitua ou complemente o template genérico de DATABASE.md com:

```markdown
# Guias de Banco de Dados

## Motor(es) de Persistência Detectados

| Motor | Uso | Localização dos dados |
|-------|-----|-----------------------|
| [MariaDB / jsonq / ambos] | [toda a app / módulo X] | [caminho real] |

---

## mameyugo/jsonq — Motor de Persistência JSON

### O que é
Extensão PHP escrita em Rust que fornece armazenamento em arquivos `.json` com
queries estilo MongoDB, indexação, validação de esquema e transações ACID.
Requer a extensão nativa `jsonq.so` carregada no PHP.

### Requisitos
- PHP >= 8.1
- Extensão `ext-jsonq` instalada (`php -m | grep jsonq`)
- Pasta de dados com permissão de escrita para o PHP

### Estrutura de Dados Detectada

```
[caminho raiz dos dados — ex: data/]
├── [colecao1].json          # Equivale a uma tabela/coleção
├── [colecao2].json
├── indexes/                 # Índices autogerados pelo JsonQ — NÃO editar
│   ├── [colecao1]/
│   └── [colecao2]/
└── schemas/                 # Esquemas de validação (se existirem)
    └── [colecao1].schema.json
```

### Coleções Existentes

| Coleção (arquivo .json) | Propósito | Campos principais detectados |
|------------------------|-----------|------------------------------|
| [nome real] | [descrição] | [campos inferidos do JSON] |

### Padrão de Acesso no Projeto

```php
// Padrão detectado nos Repositories — ajustar conforme o código real

// Leitura com query
$resultado = JsonQ::open('data/[colecao].json')
    ->from('[colecao]')
    ->where('campo', '=', $valor)
    ->get();

// Inserção
JsonQ::open('data/[colecao].json')
    ->insert(['campo' => $valor, ...]);

// Atualização
JsonQ::open('data/[colecao].json')
    ->from('[colecao]')
    ->where('id', '=', $id)
    ->update(['campo' => $novoValor]);

// Remoção
JsonQ::open('data/[colecao].json')
    ->from('[colecao]')
    ->where('id', '=', $id)
    ->delete();

// Transação ACID (se o projeto as utiliza)
$db = JsonQ::open('data/[colecao].json');
$db->beginTransaction();
try {
    $db->insert([...]);
    $db->commit();
} catch (\Exception $e) {
    $db->rollback();
    throw $e;
}
```

### Regras Obrigatórias do Projeto

- [ ] **Nunca editar os `.json` de dados diretamente** — usar sempre a API do JsonQ
- [ ] **Nunca editar a pasta `indexes/`** — é autogerenciada pelo JsonQ
- [ ] **IDs**: [descrever a política de IDs detectada — UUID, autoincremento manual, etc.]
- [ ] **Validação**: realizar sempre no Service/ValueObject antes de persistir;
      JsonQ não valida tipos por padrão salvo se um schema for configurado
- [ ] **Concorrência**: JsonQ usa file locking — documentar se há processos concorrentes
- [ ] **Backups**: os arquivos `.json` são a fonte de verdade — incluir na política de backup

### Quando Usar jsonq vs [outro BD se coexistir]

> ⚠️ Se o projeto usa tanto MariaDB quanto jsonq, documentar aqui quais módulos
> usam cada motor e a razão da coexistência.

| Cenário | Motor recomendado |
|---------|------------------|
| [caso de uso do projeto] | jsonq / MariaDB |

### Performance

- JsonQ usa SIMD parsing (simd-json) e cache Arc com invalidação por mtime
- Os índices hash permitem lookups O(1) em campos indexados
- Para coleções grandes (>10k registros), verificar se há índices definidos
- O file locking pode ser gargalo com alta concorrência

### Checklist de Design com jsonq

- [ ] Pasta de dados fora do diretório público (`public/`, `web/`)
- [ ] Permissões corretas na pasta de dados (escrita apenas para PHP, sem acesso web)
- [ ] Coleções com esquema de validação definido se o jsonq suportar
- [ ] Política de IDs consistente em todo o projeto
- [ ] Pasta `indexes/` no `.gitignore` (regerada automaticamente)
- [ ] Arquivos `.json` de dados no `.gitignore` se contiverem dados sensíveis
- [ ] Backups automatizados dos arquivos `.json`
```

---

### `.ai/DECISIONS/[YYYY-MM-DD]-NNN-[titulo].md`

Para cada decisão arquitetural importante detectada no código, gere um ADR:

```markdown
# [NNN]: [Título da Decisão]

**Data**: [YYYY-MM-DD]
**Status**: Aceita | Proposta | Substituída por NNN

## Contexto
[Qual problema ou necessidade motivou esta decisão — inferido do código]

## Decisão
[O que foi decidido implementar]

## Consequências

**Positivas:**
- [consequência]

**Negativas / Trade-offs:**
- [consequência]

## Alternativas Descartadas
1. **[Alternativa]**: [por que não foi escolhida]

## Arquivos Relacionados
- [Caminhos reais no projeto]
```

---

## 🔧 Instruções Específicas por Stack

### Se detectar PHP + Symfony/Framework Customizado

- Analise `composer.json` para versão do PHP e dependências
- Mapeie a estrutura de módulos em `app/modulos/` ou `src/`
- Detecte o padrão de Controllers (thin vs fat), Services e Repositories
- Identifique se são usados Value Objects com autovalidação
- Verifique se `phpstan.neon` existe e extraia o nível configurado
- Extraia comandos de `composer.json` → `scripts`
- Detecte o sistema de traduções (Symfony Translator, `lang()` customizado, etc.)
- Documente a política de COMMENT em campos de BD se existir nos `.sql`

**Se `mameyugo/jsonq` também for detectado** (pode coexistir com MariaDB ou ser a única persistência):
- Verifique se `extension=jsonq.so` está habilitada na configuração PHP
- Identifique a pasta raiz de dados JSON (habitualmente `data/` ou `storage/json/`)
- Liste os arquivos `.json` existentes — cada um equivale a uma "coleção/tabela"
- Detecte se há pasta `indexes/` autogerada (indica indexação ativa)
- Encontre o padrão de acesso nos Repositories: `JsonQ::open('caminho/colecao.json')`
- Determine se jsonq é usado para **toda** a persistência ou apenas em módulos específicos
- Documente os esquemas JSON implícitos lendo a estrutura dos arquivos de dados
- Identifique se são usadas transações JsonQ (`->beginTransaction()`, `->commit()`, `->rollback()`)
- Gere `.ai/DATABASE.md` com a seção JsonQ conforme o template específico acima

### Se detectar Node.js / TypeScript

- Analise `package.json` dependencies e scripts
- Mapeie se é Express, Fastify, NestJS ou outro
- Detecte se existe `tsconfig.json` e extraia `strict`, `target`, `paths`
- Verifique `jest.config.*` ou `vitest.config.*`
- Identifique se há monorepo (Turborepo, Nx, workspaces)

### Se detectar Python

- Analise `requirements.txt`, `pyproject.toml` ou `Pipfile`
- Detecte o framework: FastAPI, Django, Flask
- Verifique `mypy.ini` ou `pyproject.toml` [mypy] para tipos
- Extraia configuração do pytest

### Se detectar múltiplos stacks (monorepo)

- Documente cada um separadamente em seções de ARCHITECTURE.md
- Identifique as fronteiras de comunicação entre stacks
- Gere ADR específico sobre a decisão de monorepo

---

## 🔗 Integração com Documentação Existente

Se encontrar arquivos de documentação preexistentes, **não os exclua**. Em vez disso:

| Encontrado | Ação |
|------------|------|
| `.ai-docs/*.md` | Referencie de `.ai/*.md` e sincronize o conteúdo |
| `.github/copilot-instructions.md` | Mantenha e adicione referência a `.ai/` |
| `.cursorrules` | Mantenha e adicione referência a `.ai/` |
| `CLAUDE.md` | Mantenha e adicione referência a `.ai/` |
| `README.md` | Extraia informações técnicas para `AGENT.md` |

No `AGENT.md`, documente quais arquivos existem para cada ferramenta:

```markdown
## Compatibilidade com Ferramentas de IA
- **GitHub Copilot**: `.github/copilot-instructions.md` + `.ai-docs/*.md`
- **Cursor**: `.cursorrules` ou `.ai/*.md`
- **Gemini / Claude**: Este `AGENT.md` + `.ai/*.md`
```

---

## 📊 Resumo da Saída Esperada

Ao finalizar a análise, forneça um resumo estruturado:

```markdown
## ✅ Documentação Gerada

### Stack Detectado
- **Linguagem principal**: [...]
- **Framework**: [...]
- **BD / Persistência**: [...] *(se jsonq detectado: "mameyugo/jsonq — arquivos JSON" ou "MariaDB + mameyugo/jsonq")*
- **Testes**: [...]
- **DevOps**: [...]

### Arquivos Gerados
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

### ADRs Gerados
- [x] `.ai/DECISIONS/[data]-001-[decisao].md`
- [x] `.ai/DECISIONS/[data]-002-[decisao].md`
*(Se jsonq detectado: gerar ADR específico sobre a decisão de usar persistência em arquivos JSON e seus trade-offs em relação a um BD relacional)*

### Documentação Preexistente Detectada
| Arquivo | Status |
|---------|--------|
| `.ai-docs/*.md` | Referenciado de `.ai/` |
| `.github/copilot-instructions.md` | Mantido, referência adicionada |

### ⚠️ Áreas sem Informação Suficiente
- [ ] **[Área]**: [o que falta e recomendação]
- [ ] **[Área]**: [o que falta e recomendação]

### 🔍 Inconsistências Detectadas
- **[Inconsistência]**: [descrição e recomendação]

## 🚀 Próximos Passos Recomendados
1. Revisar e ajustar os arquivos gerados
2. Completar as seções marcadas como incompletas
3. Criar o primeiro ADR para a decisão mais importante do projeto
4. Compartilhar com a equipe para validação
5. Atualizar a documentação a cada mudança arquitetural significativa
```

---

## 🎯 Comportamento Esperado do Agente

- **Não modificar código existente**: apenas leitura, nunca escrita em arquivos-fonte
- **Específico, não genérico**: se PHPUnit for encontrado, não escreva "um framework de testes"; escreva "PHPUnit 11"
- **Documentar suposições**: se algo não estiver claro no código, indique explicitamente com `> ⚠️ Suposição: ...`
- **Sinalizar inconsistências**: se encontrar padrões contraditórios (ex: alguns módulos com testes encapsulados e outros não), documente
- **Priorizar o crítico**: gere primeiro AGENT.md, ARCHITECTURE.md e SECURITY.md; o restante pode ser gerado iterativamente

---

## 🚀 Inicie a Análise

Analise o projeto atual seguindo as três fases descritas e gere a documentação na ordem recomendada. Se alguma seção não tiver informações suficientes no código, deixe-a com uma nota `> ℹ️ Pendente de preenchimento manual` em vez de inventar conteúdo.
