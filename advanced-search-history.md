# Advanced Search in Chat History

## O que e
Permitir que usuarios encontrem informacoes em conversas antigas.

## Implementacao
- Full-text search (PostgreSQL tsvector ou Elasticsearch)
- Filtros por data, tipo de midia, ou conversa especifica
- Semantic search: usar embeddings para buscar por significado

## UX/UI
- Barra de busca global com atalho de teclado
- Highlights dos termos buscados nas mensagens
- Preview do contexto da mensagem encontrada