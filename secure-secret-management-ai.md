# Secure Secret Management for AI - Gerenciamento Seguro de Segredos para IA

## O que e
Práticas e ferramentas para permitir que IAs utilizem credenciais (senhas, API keys) sem nunca expô-las em texto plano, logs ou prompts.

## Arquitetura Segura
- NUNCA colar senhas diretamente no prompt do chat.
- Usar cofres de segredos (HashiCorp Vault, AWS Secrets Manager, Azure Key Vault).
- O agente recebe apenas um token de acesso temporário e com escopo limitado (ex: "ler apenas esta tabela").

## Implementação
- Injeção de Segredos: O backend injeta a credencial no ambiente de execução do agente, não no contexto do LLM.
- Máscara de Dados: Ferramentas de DLP (Data Loss Prevention) que detectam e ofuscam padrões de CPF, cartão de crédito ou senhas antes de enviar ao LLM.
- Client-Side Encryption: Criptografar dados sensíveis no navegador antes de enviar para processamento.

## Nota sobre "Jailbreaks"
Técnicas que tentam forçar o LLM a revelar segredos do sistema (como prompts maliciosos) devem ser mitigadas com:
- Validação rigorosa de output
- Sandboxing de execução
- Princípio do menor privilégio nas credenciais fornecidas ao agente
