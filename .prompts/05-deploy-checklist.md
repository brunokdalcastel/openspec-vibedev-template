# Prompt 05 — Checklist de Deploy

> **Quando usar:** ANTES de subir para produção (staging ou production).
> Funciona como um "Pre-flight Check" antes da decolagem.

## Como usar

1. Copie o bloco abaixo
2. Cole no Claude Code
3. O AI vai gerar um checklist personalizado para o seu projeto

---

## Prompt — Copie daqui ↓

```
Leia estes arquivos:
1. AI-INSTRUCTIONS.md
2. openspec/config.yaml
3. openspec/project.md
4. Todos os specs em openspec/specs/

Gere um checklist de deploy COMPLETO para este projeto.

O checklist deve cobrir:

## Segurança  
- [ ] Todas as variáveis de ambiente configuradas (nenhum secret no código)
- [ ] .env NÃO está no repositório (.gitignore)
- [ ] CORS configurado (nada de wildcard * em produção)
- [ ] Security headers ativos (CSP, HSTS, X-Frame-Options, etc)
- [ ] Rate limiting configurado
- [ ] Validação de input em todas as rotas
- [ ] Auth usando biblioteca testada (não custom)
- [ ] Cookies com httpOnly + Secure + SameSite

## Banco de Dados
- [ ] Connection string via variável de ambiente
- [ ] SSL/TLS habilitado para conexão remota
- [ ] Usuário do DB com privilégios mínimos (não root)
- [ ] Migrations testadas em staging antes de produção
- [ ] Backup automatizado configurado
- [ ] Backup criptografado

## Código
- [ ] Sem console.log / print de debug em produção
- [ ] Error handling em todo código assíncrono
- [ ] Stack traces NÃO expostos ao cliente
- [ ] npm audit / pip audit sem vulnerabilidades críticas
- [ ] Lock files commitados (package-lock.json / poetry.lock)

## Infraestrutura
- [ ] HTTPS obrigatório (certificado válido)
- [ ] Logs centralizados e estruturados
- [ ] Monitoramento configurado (uptime, erros)
- [ ] DNS configurado corretamente
- [ ] Sem portas desnecessárias expostas

## LGPD
- [ ] Consentimento explícito implementado
- [ ] Usuários podem exportar seus dados
- [ ] Usuários podem solicitar exclusão
- [ ] Data minimization (coleta apenas o necessário)

Adicione itens específicos baseados no stack definido em openspec/project.md.
Para cada item, explique por que é importante em termos simples.
```
