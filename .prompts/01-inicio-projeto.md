# Prompt 01 — Início do Projeto

> **Quando usar:** Na primeira vez que abrir o AI neste projeto, para configurar o contexto.

## Como usar

1. Abra o Claude Code (ou seu AI)
2. Copie e cole o bloco abaixo
3. Substitua os `[PLACEHOLDERS]` pelas suas informações
4. O AI vai ajudar a preencher o `project.md`

---

## Prompt — Copie daqui ↓

```
Antes de começar, leia estes 3 arquivos obrigatórios:
1. AI-INSTRUCTIONS.md
2. openspec/config.yaml
3. openspec/project.md

Agora me ajude a preencher o openspec/project.md com os detalhes do meu projeto.

Informações do projeto:
- Nome: [NOME DO PROJETO]
- Descrição: [DESCREVA O QUE O PROJETO FAZ EM 1-2 FRASES]
- Stack frontend: [React / Next.js / Vue / Svelte / ou "não sei, me sugira"]
- Stack backend: [Node.js / Python / Go / ou "não sei, me sugira"]
- Banco de dados: [PostgreSQL / MySQL / MongoDB / ou "não sei, me sugira"]
- Auth: [NextAuth / Supabase / Auth0 / ou "não sei, me sugira"]
- Deploy: [Vercel / Azure / AWS / Railway / ou "não sei, me sugira"]
- AI que vou usar: [Claude Code / Cursor / Codex]

Considerações:
- Eu sou de infraestrutura, não sou desenvolvedor. Preciso de explicações simples.
- Segurança é prioridade máxima.
- Preciso seguir a LGPD.

Preencha o project.md mantendo as convenções e regras de segurança que já estão lá.
Explique cada escolha que fizer em termos simples.
```
