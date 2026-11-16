# Database Design for AI Chat

## Schema Basico
- Users: id, email, password_hash, created_at
- Conversations: id, user_id, title, model_used, created_at
- Messages: id, conversation_id, role, content, tokens_used, created_at

## Otimizacoes
- Indexes em user_id e conversation_id para buscas rapidas
- Partitioning de tabelas de mensagens por data para escalabilidade
- Soft deletes para permitir recuperacao de dados

## Escalabilidade
- Read replicas para consultas de historico
- Archive de conversas antigas para storage frio (S3)