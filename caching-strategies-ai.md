# Caching Strategies

## Niveis de Cache
- Frontend: React Query, localStorage para rascunhos
- Backend: Redis para respostas de LLM identicas ou RAG retrievals
- CDN: Cache de assets estaticos e documentos publicos

## Invalidacao
- TTL (Time-To-Live) baseado no tipo de dado
- Invalidacao por evento (ex: quando documento e atualizado)

## Otimizacao de Tokens via Cache
- Cache de embeddings: Nao re-embeddar documentos identicos
- Cache de respostas: Para perguntas frequentes (FAQ)