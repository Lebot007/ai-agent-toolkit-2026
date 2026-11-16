# Workflow Orchestration - Orquestração de Fluxos de Trabalho Humano-IA

## O que e
Sistemas que coordenam tarefas complexas envolvendo múltiplos passos humanos e de IA.

## Arquitetura
- Engine de workflow (Temporal, Airflow, LangGraph)
- Nós de decisão: "Se confiança < 80%, pedir revisão humana"
- State machine para rastrear o progresso de cada item

## Padrões
- Human-in-the-loop (HITL): Pausar automação para aprovação humana
- Escalation: Se a IA falhar N vezes, escalar para humano
- Parallel Execution: IA processa múltiplos itens enquanto humano revisa outro

## Casos de Uso
- Processamento de sinistros de seguro
- Triagem de candidatos em RH
- Moderação de conteúdo em escala
