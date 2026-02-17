# Project Context

## Overview
<!-- PREENCHA: Descreva a aplicação -->
<!-- Ex: "SaaS para gestão de contratos com dashboard e integração de pagamentos" -->

## Tech Stack
<!-- PREENCHA: Descomente e ajuste as linhas do seu stack -->

### Frontend
<!-- - React / Next.js / Vue / Svelte / Astro -->
<!-- - Tailwind CSS / Shadcn/ui / Material UI -->

### Backend
<!-- - Node.js (Express / Fastify / Hono) -->
<!-- - Python (FastAPI / Django) -->
<!-- - Go / Rust -->

### Database
<!-- - PostgreSQL / MySQL / SQLite -->
<!-- - Supabase / PlanetScale / Neon -->
<!-- - MongoDB / Redis (cache) -->

### ORM / Query Builder
<!-- - Prisma / Drizzle / TypeORM -->
<!-- - SQLAlchemy / Django ORM -->

### Auth
<!-- - NextAuth.js / Supabase Auth / Auth0 / Clerk / Lucia -->

### Deploy
<!-- - Vercel / Railway / Fly.io -->
<!-- - Azure App Service / AWS -->
<!-- - Docker + VPS -->

### AI Tools
<!-- - Claude Code / Cursor / Codex / Windsurf -->

## Architecture
<!-- PREENCHA: Ajuste ao seu padrão -->
- API-first design
- Server-side rendering onde possível
- Database migrations versionadas
- Separation of concerns (routes → services → repositories)

## Conventions

### Naming
- Components: PascalCase (`UserProfile.tsx`)
- Files: kebab-case (`user-profile.ts`)
- API routes: RESTful (`/api/v1/users/:id`)
- Database: snake_case (`user_profiles`)
- Branches: `feat/`, `fix/`, `security/`

### Code Style
- Strict types (TypeScript strict mode / Python type hints)
- Linter + formatter configurados (ESLint+Prettier / Ruff / etc.)
- Funções pequenas e testáveis
- Comentários explicam o "porquê", não o "como"

### SECURITY RULES (NON-NEGOTIABLE)
1. TODA entrada validada com schema library (Zod/Joi/Pydantic)
2. SEMPRE ORM ou prepared statements — NUNCA string concatenation SQL
3. SEMPRE sanitizar output contra XSS
4. NUNCA implementar auth custom — usar biblioteca testada
5. Verificar permissões no SERVIDOR, não só no frontend
6. ZERO secrets no código — .env + vault, .env no .gitignore
7. CORS restritivo — NUNCA wildcard em produção
8. Rate limiting em TODOS endpoints públicos
9. NUNCA expor stack traces ou erros internos ao cliente
10. Security headers obrigatórios (CSP, HSTS, X-Frame-Options)
11. File uploads: validar tipo (magic bytes), tamanho, sanitizar nome
12. Dependências: audit em CI, pin versions, renovate habilitado
13. LGPD: consentimento explícito, data minimization, direito a exclusão

### AI-Assisted Development Rules
- O AI DEVE seguir as security rules acima mesmo sem ser pedido
- O AI DEVE adicionar validação de input em toda rota automaticamente
- O AI NÃO DEVE gerar código que desabilite segurança "para testar"
- O AI DEVE incluir error handling em todo código assíncrono
- O AI DEVE gerar testes para lógica de negócio e validações

## Team
<!-- PREENCHA: -->
<!-- - Developer principal não é especialista em segurança -->
<!-- - Uso intensivo de AI para geração de código -->
<!-- - Foco: velocidade com guardrails de segurança -->
