# Prompt 04 — Gerar Testes

> **Quando usar:** Para criar testes automatizados baseados nas specs.
> Ideal após implementar uma feature com `/opsx:apply`.

## Como usar

1. Copie o bloco abaixo
2. Substitua `[ÁREA]` pela parte que quer testar
3. Cole no Claude Code

---

## Prompt — Copie daqui ↓

```
Leia estes arquivos:
1. AI-INSTRUCTIONS.md
2. openspec/config.yaml  
3. openspec/specs/[ÁREA]/spec.md

Com base nos cenários definidos na spec de [ÁREA], crie testes automatizados que cubram:

1. ✅ Cenários de SUCESSO (happy path)
   - Cada cenário da spec deve ter pelo menos 1 teste de sucesso

2. ❌ Cenários de ERRO 
   - Validação de input inválido (400)
   - Sem autenticação (401)
   - Sem permissão (403)
   - Recurso não encontrado (404)
   - Rate limiting (429)

3. 🔒 Cenários de SEGURANÇA
   - SQL injection (deve ser bloqueado)
   - XSS (deve ser sanitizado)
   - Acesso não autorizado (user A tentando acessar dados do user B)

Use o framework de teste adequado ao stack do projeto (veja openspec/project.md).

Explique o que cada teste faz em comentários simples.
```

## Exemplos de [ÁREA]:

| Área | O que testa |
|------|------------|
| `api` | Rotas REST, paginação, CORS |
| `auth-security` | Login, sessões, permissões |
| `backend` | Endpoints, validação, error handling |
| `database` | Queries, migrations, proteção de dados |
| `frontend` | Componentes, formulários, XSS |
