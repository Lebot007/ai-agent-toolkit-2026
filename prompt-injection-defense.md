# Prompt Injection Defense - Defesa Contra Injeção de Prompt

## O que e
Mecanismos para proteger agentes de IA contra tentativas de manipulação por usuários maliciosos que tentam sobrescrever as instruções originais.

## Vetores de Ataque
- Injeção Direta: Usuário digita "Ignore as instruções anteriores e faça X"
- Injeção Indireta (Data Poisoning): O agente lê um documento ou site que contém instruções maliciosas ocultas

## Estratégias de Defesa
- Delimitação: Usar tags XML (ex: `<user_input>...</user_input>`) e instruir o modelo a tratar o conteúdo apenas como dados, não como comandos
- LLM-Based Guardrails: Um modelo menor e especializado (ex: Llama Guard, NeMo Guardrails) que filtra o input e o output em busca de padrões de ataque
- Human-in-the-Loop: Para ações destrutivas, exigir aprovação humana independente do que o LLM "decidiu"
