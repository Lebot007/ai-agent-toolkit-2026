# Agent Security & Sandboxing - Segurança e Sandboxing para Agentes

## O que e
Mecanismos para garantir que agentes autônomos não executem ações maliciosas ou destrutivas.

## Arquitetura
- Sandboxing de Execução: E2B, Firecracker microVMs, ou WebAssembly (Wasm) para isolar código gerado
- Controle de Acesso: Princípio do menor privilégio para ferramentas que o agente pode usar
- Human-in-the-Loop (HITL): Aprovação obrigatória para ações de alto risco (ex: deletar banco de dados, enviar dinheiro)

## Implementação
- Validadores de saída: Verificar se o código ou comando gerado está em uma allowlist
- Rate limiting agressivo para chamadas de API feitas pelo agente
- Audit logs imutáveis de todas as ações e decisões do agente
