# openspec-vibedev-template

Template para projetos de **desenvolvimento com AI (vibe coding)** usando OpenSpec CLI.
Foco em **segurança por padrão** — ideal para quem **não é especialista em AppSec ou desenvolvimento**.

> **Para quem é de infra e não de dev:** pense no OpenSpec como um "runbook" para o AI.
> Assim como você usa runbooks e playbooks para padronizar operações de infra,
> o OpenSpec padroniza como o AI gera código — com regras, checklists e validações.

---

## 📋 Índice

- [O que é isso?](#-o-que-é-isso)
- [Pré-requisitos](#-pré-requisitos)
- [Quick Start — Passo a Passo](#-quick-start--passo-a-passo)
- [Como o OpenSpec funciona](#-como-o-openspec-funciona)
- [Comandos — Referência completa](#-comandos--referência-completa)
- [Fluxos de trabalho](#-fluxos-de-trabalho)
- [Instruções para a IA](#-instruções-para-a-ia)
- [Prompts prontos para usar](#-prompts-prontos-para-usar)
- [O que vem incluso](#-o-que-vem-incluso)
- [Stack agnóstico](#-stack-agnóstico)
- [Por que segurança é tão enfatizada?](#-por-que-segurança-é-tão-enfatizada)
- [Dicas para economizar sessões do Claude Code](#-dicas-para-economizar-sessões-do-claude-code)
- [Glossário](#-glossário)
- [Estrutura de pastas](#-estrutura-de-pastas)

---

## 🤔 O que é isso?

**OpenSpec** é uma ferramenta CLI que organiza o trabalho entre você e o AI.

### Analogia para quem é de infra:

| Conceito de Infra | Equivalente no OpenSpec |
|---|---|
| **Runbook/Playbook** | As **specs** (especificações) — regras que o AI segue |
| **Change Request / RFC** | O comando **`/opsx:new`** — cria uma "solicitação de mudança" |
| **Plano de implementação** | Os **artifacts** (proposal, design, tasks) |
| **Checklist pré-deploy** | O comando **`/opsx:verify`** — valida se tudo foi feito |
| **Post-mortem / documentação** | O comando **`/opsx:archive`** — documenta e finaliza |

### O problema que ele resolve:

Sem o OpenSpec, você pede algo para o AI e ele gera código "sem rumo" — sem seguir padrões, sem segurança, sem documentação. Cada sessão é uma "folha em branco".

Com o OpenSpec, o AI:
1. **Lê as specs** (regras do projeto) ANTES de escrever código
2. **Cria um plano** (proposal + design + tasks) ANTES de implementar
3. **Segue as regras de segurança** que você definiu
4. **Documenta tudo** automaticamente

---

## 📦 Pré-requisitos

### 1. Node.js 20.19+

```bash
# Verificar se já tem instalado:
node --version

# Se não tiver, baixe em: https://nodejs.org
# Escolha a versão LTS (Long Term Support)
```

### 2. OpenSpec CLI

```bash
npm install -g @fission-ai/openspec@latest
```

### 3. Um AI coding assistant

O OpenSpec funciona com qualquer um destes (entre outros):
- **Claude Code** (recomendado)
- **Cursor**
- **Windsurf**
- **GitHub Copilot Chat**
- **Codex CLI**

> **Nota:** Para a melhor experiência, use modelos de alto raciocínio (Claude Opus, GPT 4o, etc).

---

## 🚀 Quick Start — Passo a Passo

Siga exatamente estes passos. Cada um é explicado em detalhe.

### Passo 1: Clone o template

```bash
git clone https://github.com/brunokdalcastel/openspec-vibedev-template.git meu-app
cd meu-app
```

> **O que isso faz:** Baixa uma cópia do template para a sua máquina, dentro de uma pasta chamada `meu-app` (troque pelo nome do seu projeto).

### Passo 2: Remove o histórico do template e inicia o seu

```bash
# No Linux/Mac:
rm -rf .git

# No Windows (PowerShell):
Remove-Item -Recurse -Force .git

# Depois, em qualquer OS:
git init
```

> **O que isso faz:** Remove o histórico git do template (que é meu) e inicia um repositório novo que é do SEU projeto.

### Passo 3: Inicializa o OpenSpec

```bash
openspec init --tools claude
```

Opções de tools:
- `claude` — para Claude Code
- `cursor` — para Cursor
- `claude,cursor` — para usar ambos
- Execute `openspec init --help` para ver todas as opções

> **O que isso faz:** Cria os arquivos de configuração que o AI vai ler automaticamente.
> O OpenSpec injeta instruções no seu AI coding assistant para que ele entenda os comandos `/opsx:`.

### Passo 4: Personalize o contexto do projeto

Abra o Claude Code (ou seu AI) e digite:

```
Leia o arquivo openspec/project.md e me ajude a preencher com os detalhes deste projeto.
Meu stack é [descreva aqui o que você vai usar ou pergunte sugestões].
```

> **O que isso faz:** O arquivo `openspec/project.md` é o "perfil" do seu projeto. Ele diz ao AI que tecnologias você usa, suas convenções, e as regras de segurança. Preencher isso ECONOMIZA sessões futuras, porque o AI já vai saber o contexto.

### Passo 5: Comece a trabalhar!

No Claude Code, digite:

```
/opsx:new add-user-auth
```

E siga o fluxo:

```
/opsx:ff        ← Gera todos os documentos de planejamento
/opsx:apply     ← Implementa o código
/opsx:verify    ← Verifica se tudo está correto
/opsx:archive   ← Finaliza e documenta
```

---

## 🔄 Como o OpenSpec funciona

### O ciclo de vida de uma mudança:

```
    ┌─────────────────────────────────────────────────────────┐
    │                    FLUXO DO OPENSPEC                     │
    │                                                          │
    │   1. CRIAR MUDANÇA ─────── /opsx:new nome-da-feature    │
    │          │                                                │
    │          ▼                                                │
    │   2. PLANEJAR ──────────── /opsx:ff (gera tudo de vez)  │
    │      │                     ou /opsx:continue (passo a    │
    │      │                        passo)                     │
    │      │                                                   │
    │      │  Gera automaticamente:                            │
    │      │  ✓ proposal.md  → O que + por quê                │
    │      │  ✓ specs/       → Requisitos detalhados           │
    │      │  ✓ design.md    → Como implementar                │
    │      │  ✓ tasks.md     → Checklist de tarefas            │
    │      │                                                   │
    │          ▼                                                │
    │   3. IMPLEMENTAR ───────── /opsx:apply                   │
    │      │  O AI escreve o código seguindo o plano           │
    │      │                                                   │
    │          ▼                                                │
    │   4. VERIFICAR ─────────── /opsx:verify (opcional)       │
    │      │  Valida se o código bate com as specs             │
    │      │                                                   │
    │          ▼                                                │
    │   5. FINALIZAR ─────────── /opsx:archive                 │
    │      Documenta e organiza. Pronto para a próxima.        │
    └─────────────────────────────────────────────────────────┘
```

### Onde as coisas ficam:

```
openspec/
├── config.yaml          ← Regras que o AI é OBRIGADO a seguir
├── project.md           ← Contexto do projeto (stack, convenções)
├── specs/               ← Fonte da verdade (como o sistema funciona)
│   ├── api/spec.md
│   ├── auth-security/spec.md
│   ├── backend/spec.md
│   ├── database/spec.md
│   └── frontend/spec.md
└── changes/             ← Mudanças em andamento
    ├── add-user-auth/   ← Cada feature vira uma pasta
    │   ├── proposal.md
    │   ├── specs/
    │   ├── design.md
    │   └── tasks.md
    └── archive/         ← Mudanças finalizadas ficam aqui
```

---

## 📖 Comandos — Referência completa

### Tabela resumo

| Comando | O que faz | Quando usar |
|---------|-----------|-------------|
| `/opsx:explore` | Investigar ideias sem compromisso | Quando não sabe por onde começar |
| `/opsx:new` | Criar uma nova mudança | Início de feature/fix/refactor |
| `/opsx:continue` | Criar próximo artefato (um de cada vez) | Quando quer revisar cada passo |
| `/opsx:ff` | Criar TODOS os artefatos de planejamento | Quando sabe o que quer e quer ir rápido |
| `/opsx:apply` | Implementar as tarefas (escrever código) | Depois do planejamento |
| `/opsx:verify` | Validar que implementação bate com o plano | Antes de finalizar |
| `/opsx:sync` | Mesclar specs da mudança no principal | Raramente necessário (archive faz isso) |
| `/opsx:archive` | Finalizar e documentar a mudança | Quando a feature está pronta |
| `/opsx:bulk-archive` | Finalizar várias mudanças de uma vez | Quando acumulou mudanças prontas |
| `/opsx:onboard` | Tutorial guiado do OpenSpec | Primeira vez usando |

### Detalhamento de cada comando

#### `/opsx:explore` — Explorar ideias

Use quando você não tem certeza do que quer fazer, ou precisa investigar o código antes de decidir.

```
Você: /opsx:explore

AI:   O que você gostaria de explorar?

Você: Como está a autenticação do sistema hoje?

AI:   Deixa eu investigar...
      [Analisa o código]
      
      Encontrei que o sistema usa sessão baseada em cookies.
      Podemos melhorar com JWT, OAuth2, ou expandir o atual.
      Qual direção te interessa?

Você: JWT. Vamos criar uma mudança para isso.

AI:   Pronto! Execute /opsx:new add-jwt-auth para começar.
```

> **Dica:** Nenhum arquivo é criado durante exploração. Serve só para pensar.

#### `/opsx:new` — Criar uma mudança

```bash
/opsx:new nome-da-mudança

# Exemplos:
/opsx:new add-user-auth
/opsx:new fix-login-redirect
/opsx:new add-dashboard
```

> **Boas práticas de nomes:**  
> ✅ `add-dark-mode`, `fix-login-bug`, `implement-2fa`  
> ❌ `update`, `changes`, `wip`, `feature-1`

#### `/opsx:ff` — Fast-forward (gera tudo de vez)

```
Você: /opsx:ff

AI:   Gerando artefatos de planejamento...
      ✓ proposal.md  — o que vamos fazer e por quê
      ✓ specs/       — requisitos e cenários
      ✓ design.md    — abordagem técnica
      ✓ tasks.md     — checklist de implementação
      
      Pronto para implementar! Execute /opsx:apply.
```

> **Use quando:** Você sabe exatamente o que quer. É o mais rápido.

#### `/opsx:continue` — Um passo de cada vez

```
Você: /opsx:continue

AI:   Status dos artefatos:
      ✓ proposal    (feito)
      ◆ specs       (pronto para criar)
      ◆ design      (pronto para criar)
      ○ tasks       (bloqueado — precisa de specs)
      
      Criando specs...
      ✓ Criado!
      
      Próximo disponível: design, tasks
      Execute /opsx:continue para o próximo.
```

> **Use quando:** Quer revisar e ajustar cada documento antes de ir adiante.

#### `/opsx:apply` — Implementar

```
Você: /opsx:apply

AI:   Implementando add-user-auth...
      
      Lendo tasks.md:
      - [ ] 1.1 Criar modelo de usuário
      - [ ] 1.2 Implementar rota de registro
      - [ ] 1.3 Adicionar validação de input
      
      Trabalhando no 1.1...
      [Cria os arquivos]
      ✓ 1.1 Concluído
      
      Trabalhando no 1.2...
      ...
```

> **Ponto importante:** Se você precisar interromper, o AI sabe de onde parou. Basta executar `/opsx:apply` novamente.

#### `/opsx:verify` — Verificar o trabalho

```
Você: /opsx:verify

AI:   Verificando add-user-auth...
      
      COMPLETUDE
      ✓ Todas as 8 tarefas concluídas
      ✓ Todos os requisitos implementados
      ⚠ Cenário "timeout de sessão" sem teste
      
      CORREÇÃO
      ✓ Implementação bate com as specs
      ✓ Edge cases tratados
      
      COERÊNCIA
      ✓ Decisões de design refletidas no código
      ⚠ Design menciona "eventos" mas código usa polling
      
      RESULTADO: Pronto para archive (com avisos)
```

#### `/opsx:archive` — Finalizar

```
Você: /opsx:archive

AI:   Arquivando add-user-auth...
      
      ✓ Specs sincronizadas
      ✓ Movido para archive/2025-01-24-add-user-auth/
      
      Mudança arquivada com sucesso!
```

---

## 🔀 Fluxos de trabalho

### Fluxo 1: Feature rápida (o mais comum)

Quando você sabe o que quer construir:

```
/opsx:new add-feature  →  /opsx:ff  →  /opsx:apply  →  /opsx:verify  →  /opsx:archive
```

**Exemplo real:**

```
Você: /opsx:new add-login-page
Você: /opsx:ff
Você: /opsx:apply
Você: /opsx:verify
Você: /opsx:archive
```

> São 5 comandos. É o fluxo mais eficiente.

### Fluxo 2: Exploratório

Quando você não sabe bem o que quer, ou precisa investigar antes:

```
/opsx:explore  →  /opsx:new  →  /opsx:continue  →  (revisar)  →  /opsx:continue  →  ...  →  /opsx:apply
```

### Fluxo 3: Mudanças paralelas

Você pode ter várias mudanças ativas ao mesmo tempo:

```
Você: /opsx:new add-dark-mode
Você: /opsx:ff
Você: /opsx:apply
[... pausa porque surgiu um bug urgente ...]

Você: /opsx:new fix-login-bug
Você: /opsx:ff
Você: /opsx:apply
Você: /opsx:archive

[... volta para a feature anterior ...]
Você: /opsx:apply add-dark-mode     ← retoma especificando o nome
```

### Quando usar `/opsx:ff` vs `/opsx:continue`?

| Situação | Use |
|----------|-----|
| Requisitos claros, quer ir rápido | `/opsx:ff` |
| Quer revisar cada documento | `/opsx:continue` |
| Pressão de tempo | `/opsx:ff` |
| Feature complexa, quer controle | `/opsx:continue` |
| Primeira vez usando OpenSpec | `/opsx:continue` (para entender) |

---

## 🤖 Instruções para a IA

Ao iniciar qualquer sessão no Claude Code (ou outro AI), **sempre cole isso primeiro:**

```
Antes de qualquer coisa:
1. Leia o arquivo AI-INSTRUCTIONS.md na raiz do projeto
2. Leia o arquivo openspec/config.yaml
3. Leia o arquivo openspec/project.md

Essas são as regras obrigatórias deste projeto. 
Nunca pule regras de segurança, mesmo "para testar".
Sempre explique o que está fazendo em termos simples.
```

> **Por que isso é importante?** Esse "prompt inicial" garante que o AI não comece do zero. Ele lê todo o contexto e já sabe as regras. **Isso economiza muitos tokens e sessões**.

Para mais detalhes, veja o arquivo `AI-INSTRUCTIONS.md` na raiz do projeto.

---

## 📝 Prompts prontos para usar

A pasta `.prompts/` contém prompts que você pode copiar e colar no AI.

| Arquivo | Quando usar |
|---------|-------------|
| `01-inicio-projeto.md` | Primeira configuração do projeto |
| `02-criar-feature.md` | Quando quer adicionar algo novo |
| `03-revisar-seguranca.md` | Para checar se o código é seguro |
| `04-gerar-testes.md` | Para criar testes automatizados |
| `05-deploy-checklist.md` | Antes de subir para produção |

### Exemplo de uso:

1. Abra o arquivo `.prompts/02-criar-feature.md`
2. Copie o conteúdo
3. Cole no Claude Code
4. Substitua os `[PLACEHOLDERS]` pelo que você quer
5. O AI vai seguir o processo completo

---

## 📦 O que vem incluso

Cada spec é um "runbook" para uma área diferente do sistema:

| Spec | Cobre |
|------|-------|
| `frontend` | Components, forms, XSS prevention, accessibility |
| `backend` | Endpoints, input validation, error handling, logging |
| `api` | REST design, rate limiting, CORS, pagination, webhooks |
| `database` | Migrations, SQLi prevention, encryption, backups, LGPD |
| `auth-security` | Auth, sessions, headers, deps, file uploads, supply chain |

> **Analogia de infra:** Cada spec é como uma política de grupo (GPO) aplicada ao código.
> O AI é "obrigado" a seguir, assim como uma máquina no domínio é obrigada a seguir a GPO.

---

## 🔧 Stack agnóstico

Os specs NÃO forçam um stack específico. Funcionam com:

- **Frontend**: React, Next.js, Vue, Svelte, Astro, Angular...
- **Backend**: Node.js, Python, Go, Rust, PHP...
- **Database**: PostgreSQL, MySQL, SQLite, MongoDB, Supabase...
- **Auth**: NextAuth, Supabase Auth, Auth0, Clerk, Lucia...
- **Deploy**: Vercel, Railway, Fly.io, Azure, AWS, self-hosted...

Edite `openspec/project.md` para definir o stack de cada projeto.

---

## 🔒 Por que segurança é tão enfatizada?

Vibe coding gera código rápido mas o AI **não prioriza segurança por padrão**.
Sem guardrails explícitos, o AI vai:
- ❌ Pular validação de input
- ❌ Usar `SELECT *` com string concatenation (SQL Injection)
- ❌ Guardar tokens em localStorage
- ❌ Responder com stack traces completos
- ❌ Ignorar rate limiting
- ❌ Deixar CORS aberto (`*`)

Este template resolve isso com **regras no config.yaml que o AI é obrigado a seguir**
e **specs que cobrem OWASP Top 10** de forma prática.

---

## 💡 Dicas para economizar sessões do Claude Code

### 1. SEMPRE comece com contexto

Não abra o Claude Code e peça coisas do nada. Comece com:
```
Leia AI-INSTRUCTIONS.md, openspec/config.yaml e openspec/project.md antes de começar.
```

### 2. Use `/opsx:ff` em vez de `/opsx:continue` para features simples

O `/opsx:ff` faz tudo de uma vez. O `/opsx:continue` gasta mais tokens porque exige interação a cada passo.

### 3. Seja específico nos pedidos

```
# ❌ Ruim (vago, AI vai inventar):
"Faz um sistema de login"

# ✅ Bom (específico, AI segue regras):
"/opsx:new add-login-page"
"/opsx:ff"
"/opsx:apply"
```

### 4. Um feature por sessão

Não misture features na mesma sessão. Use:
```
Sessão 1: /opsx:new add-login → /opsx:ff → /opsx:apply → /opsx:archive
Sessão 2: /opsx:new add-dashboard → /opsx:ff → /opsx:apply → /opsx:archive
```

### 5. Use `/opsx:onboard` na primeira vez

Se nunca usou o OpenSpec, execute este comando no Claude Code:
```
/opsx:onboard
```
Ele vai te guiar por um tutorial interativo completo.

### 6. Limpe o contexto antes de implementar

O próprio OpenSpec recomenda: limpe a janela de contexto antes de rodar `/opsx:apply`. Isso evita que o AI se confunda com conversas anteriores.

---

## 📚 Glossário

| Termo | O que significa |
|-------|-----------------|
| **Spec** | Especificação — documento que descreve como o sistema deve se comportar |
| **Change** | Mudança proposta no sistema. Cada mudança vira uma pasta com documentos |
| **Artifact** | Documento dentro de uma mudança (proposal, design, tasks, specs) |
| **Delta spec** | Spec que descreve apenas as MUDANÇAS (adicionado/modificado/removido) |
| **Proposal** | Documento que explica O QUE vai ser feito e POR QUÊ |
| **Design** | Documento que explica COMO vai ser feito tecnicamente |
| **Tasks** | Checklist de tarefas para a implementação |
| **Archive** | Processo de finalizar uma mudança e documentar |
| **Guardrail** | Regra de segurança que o AI é obrigado a seguir |
| **Vibe coding** | Estilo de desenvolvimento onde você descreve o que quer e o AI implementa |
| **Source of truth** | Pasta `openspec/specs/` — a verdade sobre como o sistema funciona |
| **Schema** | Define a sequência de artefatos (qual vem antes de qual) |
| **SDD** | Spec-Driven Development — desenvolvimento orientado a especificações |

---

## 📁 Estrutura de pastas

```
meu-app/
├── AI-INSTRUCTIONS.md       ← Instruções que o AI lê automaticamente
├── README.md                ← Este arquivo
├── .gitignore
├── .prompts/                ← Prompts prontos para copiar e colar
│   ├── 01-inicio-projeto.md
│   ├── 02-criar-feature.md
│   ├── 03-revisar-seguranca.md
│   ├── 04-gerar-testes.md
│   └── 05-deploy-checklist.md
└── openspec/
    ├── config.yaml          ← Regras obrigatórias para o AI
    ├── project.md           ← Contexto do projeto (preencher!)
    └── specs/               ← Specs de segurança e qualidade
        ├── api/spec.md
        ├── auth-security/spec.md
        ├── backend/spec.md
        ├── database/spec.md
        └── frontend/spec.md
```

---

## 📄 Licença

MIT
