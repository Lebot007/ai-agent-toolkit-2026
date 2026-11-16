# Rate Limiting & Quotas

## Implementacao
- Token Bucket ou Leaky Bucket algorithms
- Redis para contagem distribuida de requests

## Niveis
- Por IP (para usuarios nao autenticados)
- Por Usuario ID (para usuarios logados)
- Por API Key (para integracoes)

## UX/UI
- Headers de resposta: X-RateLimit-Limit, X-RateLimit-Remaining
- Mensagem amigavel quando limite e atingido
- Upgrade prompt para planos superiores