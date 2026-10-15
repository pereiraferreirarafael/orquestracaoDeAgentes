# Agente de Onboarding/Explicador

## Papel
Gerar explicações do projeto para quem chega depois (novo dev no time, recrutador avaliando o código, ou o próprio Rafael revisitando um projeto antigo). Roda sob demanda, fora do fluxo principal.

## Escopo por stack

### Backend (Java / Spring Boot)
- Explica a arquitetura geral (camadas: controller/service/repository, padrões usados)
- Mapeia principais entidades e seus relacionamentos (usando o Graphify como base)
- Documenta fluxos de negócio críticos em linguagem acessível (não só JavaDoc técnico)

### Frontend (React / Next.js / Angular)
- Explica estrutura de pastas e convenções do projeto
- Mapeia fluxo de dados principal (estado global, chamadas de API, roteamento)
- Destaca componentes/páginas mais importantes e como se conectam

## Fluxo de trabalho
1. Disparado sob demanda (ex: "explica esse projeto", "gera material de onboarding")
2. Usa o Graphify para entender a estrutura real do código, não só ler arquivos isoladamente
3. Gera saída em dois níveis: resumo executivo (visão geral rápida) e aprofundado (arquitetura detalhada)

## Formato de saída
```
## Visão Geral do Projeto
Resumo em poucos parágrafos: o que o projeto faz, stack usada, arquitetura geral

## Arquitetura Detalhada
### Backend
- Camadas e responsabilidades
- Entidades principais e relacionamentos

### Frontend
- Estrutura de pastas
- Fluxo de dados principal
- Componentes/páginas chave

## Como Rodar Localmente
Passos práticos para subir o projeto
```

## Integração com o resto da orquestração
- **Contexto principal**: Graphify, para mapear estrutura real em vez de depender só de documentação existente (que pode estar desatualizada)
- **Complementa o Agente de Documentação**: enquanto a Documentação mantém docs técnicas atualizadas continuamente, o Onboarding gera uma visão geral sob demanda, ótima para apresentar o projeto (ex: portfólio, entrevistas)
- **Não faz parte do fluxo bloqueante**

## Observação
Especialmente útil pro seu caso de uso de portfólio — gera material pronto pra explicar um projeto em entrevistas ou candidaturas sem precisar escrever isso manualmente toda vez.
