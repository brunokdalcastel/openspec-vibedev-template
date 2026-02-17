# AI Instructions — Leia ANTES de qualquer tarefa

> **Este arquivo é obrigatório.** O AI DEVE ler este arquivo no início de cada sessão.

## Contexto do Projeto

1. Leia `openspec/project.md` para entender o stack e o contexto
2. Leia `openspec/config.yaml` para as regras obrigatórias
3. Consulte os specs em `openspec/specs/` antes de criar/modificar código

## Regras que NUNCA podem ser quebradas

1. **Segurança não é opcional.** Todas as regras em `openspec/config.yaml` são não-negociáveis
2. **Nunca desabilite segurança** — nem "para testar", nem "temporariamente"
3. **Sempre valide input** — toda entrada de usuário deve ser validada com schema library
4. **Nunca use string concatenation para SQL** — sempre ORM ou queries parametrizadas
5. **Nunca exponha erros internos** — stack traces, caminhos de arquivo, erros de DB ficam no log do servidor
6. **Nunca hardcode secrets** — use `.env` e variáveis de ambiente

## Perfil do desenvolvedor

- O desenvolvedor principal é de **infraestrutura**, não de desenvolvimento de software
- **Sempre explique** o que você está fazendo e por quê, em termos simples
- **Evite jargões** sem explicação — se usar termos técnicos de dev, explique o que significam
- **Prefira abordagens simples** e bem documentadas ao invés de soluções "elegantes" mas complexas
- As explicações devem ser em **português**

## Fluxo de trabalho esperado

1. Ao receber um pedido de feature, use o fluxo OpenSpec:
   - `/opsx:new` → `/opsx:ff` → `/opsx:apply` → `/opsx:verify` → `/opsx:archive`
2. Nunca pule o planejamento — sempre gere proposal, specs, design e tasks antes de escrever código
3. Ao finalizar, sempre execute `/opsx:verify` antes de `/opsx:archive`

## Referência dos specs

Os specs em `openspec/specs/` são a **fonte da verdade**. Antes de criar código em qualquer área, consulte:

| Área | Spec | O que contém |
|------|------|-------------|
| API REST | `openspec/specs/api/spec.md` | REST design, rate limiting, CORS, pagination |
| Auth e segurança | `openspec/specs/auth-security/spec.md` | Auth, sessions, headers, LGPD |
| Backend | `openspec/specs/backend/spec.md` | Endpoints, validação, error handling |
| Database | `openspec/specs/database/spec.md` | Migrations, queries, backups |
| Frontend | `openspec/specs/frontend/spec.md` | Components, forms, XSS, acessibilidade |
