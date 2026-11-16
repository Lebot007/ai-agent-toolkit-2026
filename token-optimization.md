# Token Optimization

## Contexto
- Truncacao Inteligente: Manter ultimas N mensagens
- Sumarizacao: Resumir mensagens antigas com LLM
- RAG: Buscar apenas trechos relevantes via vector search

## Compressao
- Minificar JSON, usar YAML
- Instrucoes concisas

## Modelos
- Modelos menores para tarefas simples
- Function Calling em vez de texto verbose

## Implementacao
- Contagem com tiktoken
- Remover mensagem mais antiga se exceder limite