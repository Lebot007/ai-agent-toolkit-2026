# Prefix Caching - Cache de Prefixo para Inferência

## O que e
Reutilização do cálculo do KV cache para prefixos de prompt idênticos entre diferentes requisições.

## Como Funciona
- Se múltiplos usuários enviam prompts que começam com o mesmo system prompt ou contexto longo, o modelo não recalcula os embeddings e o KV cache desse prefixo
- O cache é mantido na GPU para acesso de ultra-baixa latência

## Implementação
- vLLM suporta automatic prefix caching
- RadixAttention (SGLang) otimiza ainda mais o compartilhamento de prefixos em árvores de conversa
- Ideal para aplicações RAG onde o contexto do documento é o mesmo para múltiplas perguntas

## Benefícios
- Redução drástica do Time to First Token (TTFT)
- Economia de computação (FLOPs) e custo
- Permite context windows muito maiores sem penalidade de performance
