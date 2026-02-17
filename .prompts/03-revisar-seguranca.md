# Prompt 03 — Revisar Segurança

> **Quando usar:** Para checar se o código do projeto segue as regras de segurança.
> Use periodicamente, especialmente antes de deploy.

## Como usar

1. Copie o bloco abaixo
2. Cole no Claude Code
3. O AI vai analisar o código contra todas as regras de segurança das specs

---

## Prompt — Copie daqui ↓

```
Leia estes arquivos obrigatórios:
1. AI-INSTRUCTIONS.md
2. openspec/config.yaml
3. openspec/specs/auth-security/spec.md
4. openspec/specs/backend/spec.md
5. openspec/specs/api/spec.md
6. openspec/specs/database/spec.md
7. openspec/specs/frontend/spec.md

Agora faça uma revisão de segurança COMPLETA do código deste projeto.

Para CADA regra nas specs, verifique:
- O código segue a regra? (✅ Sim / ❌ Não / ⚠️ Parcial)
- Se não segue, o que precisa mudar?
- Qual é a gravidade? (CRÍTICO / ALTO / MÉDIO / BAIXO)

Organize o relatório assim:

## Resumo
- Total de regras verificadas: X
- Conformes: X
- Não conformes: X
- Parcialmente conformes: X

## Problemas Críticos (corrigir AGORA)
...

## Problemas Altos (corrigir antes do deploy)
...

## Problemas Médios (corrigir em breve)
...

## Sugestões (melhorias recomendadas)
...

Explique cada problema em termos simples, dizendo:
1. O que está errado
2. Qual o risco real (o que pode acontecer)
3. Como corrigir (com exemplo de código)
```
