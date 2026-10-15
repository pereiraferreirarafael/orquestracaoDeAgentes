# Orquestração de Agentes — Claude Code

Pipeline automático que valida o código a cada edição e antes de avançar, usando subagents e hooks do Claude Code.

> Status: os hooks ainda estão em fase de teste.

## Agentes ativos

| Agente | Disparador | Responsabilidade | Bloqueia? |
|--------|-----------|------------------|-----------|
| Revisor de Código | `PostToolUse` (Write/Edit) | Qualidade, padrões, legibilidade | Não |
| Segurança | `PostToolUse` (Write/Edit, em paralelo) | SQL injection, secrets, XSS, config insegura | Sim (Crítico/Alto) |
| Documentação | `Stop` (fim da resposta) | JavaDoc/TSDoc, README, CHANGELOG | Não |
| Teste/QA | `Stop` (fim da resposta) | Testes, cobertura, build | Sim (qualquer falha) |
| Deploy | Manual (não é hook) | Publicação com health check e rollback | Exige confirmação humana |
| Performance | Manual (antes do deploy) | N+1, queries sem paginação, bundle, re-renders | Não (recomenda se impacto Alto) |
| Dependências | Manual / periódico | CVEs, versões desatualizadas, pacotes abandonados | Recomenda se CVE Crítica |
| Monitoramento | Manual (após o deploy) | Saúde pós-deploy; recomenda rollback | Não (recomenda rollback) |
| Refatoração | Manual (sob demanda) | Melhorias de arquitetura, consultivo | Não |
| Onboarding | Manual (sob demanda) | Explicação do projeto para novos leitores | Não |

## Fluxo

```
Edição de código
   → Revisor de Código + Segurança (paralelo)
   → fim da resposta
   → Documentação + Teste/QA
   → (manual) Performance → Deploy (só após confirmação humana) → Monitoramento
   → (sob demanda) Dependências, Refatoração, Onboarding
```

O Deploy não é disparado por hook de propósito: publicar em produção exige pedido e confirmação explícitos. Só Revisor, Segurança, Documentação e QA estão ligados a hooks; os demais são chamados sob demanda (ex.: "use o agente performance"). Os hooks de um mesmo evento podem rodar em paralelo, então a ordem entre Documentação e QA não é garantida.

## Como funciona

- Cada agente é um arquivo Markdown com frontmatter YAML em `.claude/agents/` (prompt + `tools` permitidas).
- Os gatilhos estão em `.claude/settings.json` (hooks `PostToolUse` e `Stop`).
- Subagents só são carregados na inicialização: reinicie o Claude Code após copiar os arquivos e confira com `/agents`.

## Especificações

Versões mais detalhadas de cada agente (escopo, fluxo e integração) estão em `docs/especificacoes/`.

## Stack coberto

- Backend: Java, Spring Boot, JPA/Hibernate, JDBC, Maven
- Frontend: React, Next.js, Angular, TypeScript, npm
