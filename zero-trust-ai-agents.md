# Zero-Trust Architecture for AI Agents - Arquitetura de Confiança Zero para Agentes

## O que e
Aplicar o modelo "nunca confie, sempre verifique" a agentes de IA que interagem com sistemas internos.

## Princípios
- Verificação Explícita: Cada ação solicitada pelo agente deve ser autenticada e autorizada, independentemente de onde o agente esteja "rodando"
- Acesso com Menor Privilégio: O agente só tem permissão para a ação específica solicitada, nada mais
- Microssegmentação: Isolar o ambiente de execução do agente do restante da rede corporativa

## Implementação
- Service Mesh (Istio, Linkerd) para mTLS entre o agente e os serviços de backend
- Short-lived credentials: Tokens JWT que expiram em minutos, renovados apenas se a tarefa continuar
- Audit Logging imutável de todas as decisões e ações do agente
