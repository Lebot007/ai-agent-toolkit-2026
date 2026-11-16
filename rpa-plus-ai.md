# RPA + IA - Robotic Process Automation Aprimorado por IA

## O que e
Evolução do RPA tradicional (baseado em regras fixas) para RPA cognitivo, capaz de lidar com exceções e dados não estruturados.

## Arquitetura
- RPA Bot: Executa ações na UI (cliques, digitação)
- IA Brain: LLM ou modelo de visão toma decisões sobre o que fazer quando encontra uma variação não prevista
- Orquestrador: Gerencia a fila de trabalho e a interação entre bot e IA

## Casos de Uso
- Processamento de reclamações de clientes (classificar sentimento, extrair detalhes, atualizar ticket)
- Migração de dados entre sistemas legados sem API
- Conciliação bancária automática com tratamento de exceções

## Melhores Práticas
- Manter o RPA para tarefas de alto volume e baixa complexidade
- Usar IA apenas nos pontos de decisão ou extração de dados complexos
- Monitorar a taxa de exceções que exigem intervenção humana
