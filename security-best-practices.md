# Security Best Practices

## Autenticacao e Autorizacao
- JWT ou Session-based auth
- RBAC (Role-Based Access Control) para funcionalidades premium

## Protecao de Dados
- Criptografia em repouso (AES-256) e em transito (TLS 1.3)
- Sanitizacao de inputs para prevenir XSS e Injection
- Validação rigorosa de uploads (MIME type, tamanho, virus scan)

## LLM Security
- Prompt Injection prevention: Separar instrucoes de dados do usuario
- Output validation: Garantir que a IA nao vaze dados sensiveis
- Content moderation: Filtrar conteudo nocivo ou abusivo