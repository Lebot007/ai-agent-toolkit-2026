# Agent Memory Architectures - Arquiteturas de Memória para Agentes

## O que e
Sistemas que permitem aos agentes reterem, recuperarem e utilizarem informações de experiências passadas.

## Tipos de Memória
- Sensory Memory: Dados brutos de entrada (últimos segundos)
- Short-term/Working Memory: Contexto da tarefa atual (janela de tokens do LLM)
- Long-term Memory: Vetor database para recuperação semântica de longo prazo
- Episodic Memory: Registro de ações passadas e seus resultados

## Implementação
- Mem0 ou Zep para gerenciamento de memória de agentes
- Reflexion: Agente escreve resumos de experiências no final do dia
- Forgetfulness: Mecanismos para descartar informações obsoletas ou irrelevantes
