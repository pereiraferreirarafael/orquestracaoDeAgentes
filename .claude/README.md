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

## Fluxo

```
Edição de código
   → Revisor de Código + Segurança (paralelo)
   → fim da resposta
   → Documentação + Teste/QA
   → (manual) Deploy, só após confirmação humana
```

O Deploy não é disparado por hook de propósito: publicar em produção exige pedido e confirmação explícitos. Os hooks de um mesmo evento podem rodar em paralelo, então a ordem entre Documentação e QA não é garantida.

## Como funciona

- Cada agente é um arquivo Markdown com frontmatter YAML em `.claude/agents/` (prompt + `tools` permitidas).
- Os gatilhos estão em `.claude/settings.json` (hooks `PostToolUse` e `Stop`).
- Subagents só são carregados na inicialização: reinicie o Claude Code após copiar os arquivos e confira com `/agents`.

## Próximos agentes (especificações em `docs/agentes-planejados/`)

Performance, Dependências, Monitoramento pós-deploy, Refatoração e Onboarding. Todos já têm especificação, mas ainda não foram convertidos em subagents.

## Stack coberto

- Backend: Java, Spring Boot, JPA/Hibernate, JDBC, Maven
- Frontend: React, Next.js, Angular, TypeScript, npm
