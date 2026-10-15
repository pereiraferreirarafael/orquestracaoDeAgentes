# Orquestração de Agentes (Claude Code)

Pipeline de agentes para o Claude Code, voltado à stack Java/Spring Boot (backend) e React/Next.js/Angular/TypeScript (frontend).

- `.claude/agents/`: os 10 subagents (revisor de código, segurança, documentação, teste/QA, deploy, performance, dependências, monitoramento, refatoração e onboarding)
- `.claude/settings.json`: hooks que encadeiam os agentes
- `.claude/README.md`: como o pipeline funciona
- `docs/especificacoes/`: especificações detalhadas de cada agente

Para usar em outro projeto, copie a pasta `.claude/` para a raiz dele e reinicie o Claude Code.

> Status: os hooks ainda estão em fase de teste.
