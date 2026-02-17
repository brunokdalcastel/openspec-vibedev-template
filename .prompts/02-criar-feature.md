# Prompt 02 — Criar uma Feature

> **Quando usar:** Sempre que quiser adicionar algo novo ao projeto.

## Como usar

1. Copie o bloco abaixo
2. Substitua `[NOME-DA-FEATURE]` e `[DESCRIÇÃO]` 
3. Cole no Claude Code
4. O AI vai seguir o fluxo completo do OpenSpec

---

## Prompt — Copie daqui ↓

```
Antes de começar, leia:
1. AI-INSTRUCTIONS.md
2. openspec/config.yaml
3. openspec/project.md

Preciso criar uma nova feature: [DESCRIÇÃO DA FEATURE]

Siga exatamente este fluxo:

1. /opsx:new [NOME-DA-FEATURE]
2. /opsx:ff (gere todos os artefatos de planejamento)
3. Mostre-me o proposal.md e o tasks.md ANTES de implementar
4. Depois que eu aprovar, execute /opsx:apply
5. Quando terminar, execute /opsx:verify
6. Se tudo estiver OK, execute /opsx:archive

Lembre-se:
- Siga TODAS as regras de segurança do config.yaml
- Explique cada decisão em termos simples
- Consulte os specs em openspec/specs/ antes de escrever código
```

## Exemplos de features:

```
# Autenticação de usuários
[NOME-DA-FEATURE] = add-user-auth
[DESCRIÇÃO] = "Sistema de login e registro de usuários com email e senha"

# Dashboard
[NOME-DA-FEATURE] = add-dashboard  
[DESCRIÇÃO] = "Dashboard com métricas do sistema e gráficos"

# CRUD de produtos
[NOME-DA-FEATURE] = add-product-crud
[DESCRIÇÃO] = "Gerenciamento completo de produtos: criar, listar, editar e deletar"
```
