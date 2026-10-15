# Orquestração de Agentes (Claude Code)

Pipeline de agentes para o Claude Code, voltado à stack Java/Spring Boot (backend) e React/Next.js/Angular/TypeScript (frontend).

- `.claude/agents/`: subagents ativos (revisor de código, segurança, documentação, teste/QA e deploy)
- `.claude/settings.json`: hooks que encadeiam os agentes
- `.claude/README.md`: como o pipeline funciona
- `docs/agentes-planejados/`: especificações dos demais agentes (performance, dependências, monitoramento, refatoração, onboarding e versões detalhadas dos demais), ainda não ativados como subagents

Para usar em outro projeto, copie a pasta `.claude/` para a raiz dele e reinicie o Claude Code.

> Status: os hooks ainda estão em fase de teste.
