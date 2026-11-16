# Backend Architecture for AI Chat

## Padroes
- API Gateway: Roteamento, autenticacao, rate limiting
- Microservicos: Separar servico de chat, processamento de arquivos, RAG
- Message Queue: Redis/RabbitMQ para tarefas assincronas (parsing, transcricao)

## Tecnologias
- Node.js (Express, Fastify) ou Python (FastAPI, Django)
- PostgreSQL para dados estruturados (usuarios, historico)
- Redis para cache e sessoes

## Escalabilidade
- Horizontal scaling com load balancer
- Connection pooling para banco de dados
- CDN para assets estaticos e uploads