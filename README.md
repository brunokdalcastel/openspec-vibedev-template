# openspec-vibedev-template

Template para projetos de **desenvolvimento com AI (vibe coding)** usando OpenSpec CLI.
Foco em **segurança por padrão** — ideal para quem não é especialista em AppSec.

## Quick Start

```bash
# 1. Clone o template
git clone https://github.com/SEU_USER/openspec-vibedev-template.git meu-app
cd meu-app

# 2. Remove o git do template e inicia o seu
rm -rf .git
git init

# 3. Inicializa o OpenSpec com suas ferramentas
openspec init --tools claude    # ou: claude,cursor,codex

# 4. Personaliza o contexto
# Abra o AI e peça:
# "Leia openspec/project.md e me ajude a preencher com o stack e detalhes deste projeto"

# 5. Comece a trabalhar
# /opsx:new add-user-auth
# /opsx:ff
# /opsx:apply
# /opsx:archive
```

## O que vem incluso

| Spec | Cobre |
|------|-------|
| `frontend` | Components, forms, XSS prevention, accessibility |
| `backend` | Endpoints, input validation, error handling, logging |
| `api` | REST design, rate limiting, CORS, pagination, webhooks |
| `database` | Migrations, SQLi prevention, encryption, backups, LGPD |
| `auth-security` | Auth, sessions, headers, deps, file uploads, supply chain |

## Stack agnóstico

Os specs NÃO forçam um stack específico. Funcionam com:

- **Frontend**: React, Next.js, Vue, Svelte, Astro, Angular...
- **Backend**: Node.js, Python, Go, Rust, PHP...
- **Database**: PostgreSQL, MySQL, SQLite, MongoDB, Supabase...
- **Auth**: NextAuth, Supabase Auth, Auth0, Clerk, Lucia...
- **Deploy**: Vercel, Railway, Fly.io, Azure, AWS, self-hosted...

Edite `openspec/project.md` para definir o stack de cada projeto.

## Por que segurança é tão enfatizada?

Vibe coding gera código rápido mas o AI **não prioriza segurança por padrão**.
Sem guardrails explícitos, o AI vai:
- Pular validação de input
- Usar `SELECT *` com string concatenation
- Guardar tokens em localStorage
- Responder com stack traces completos
- Ignorar rate limiting
- Deixar CORS aberto

Este template resolve isso com **regras no config.yaml que o AI é obrigado a seguir**
e **specs que cobrem OWASP Top 10** de forma prática.

## Pré-requisitos

- Node.js 20.19+
- `npm install -g @fission-ai/openspec@latest`
- Um AI coding assistant (Claude Code, Cursor, Codex, etc.)
