# Agent Communication Protocols - Protocolos de Comunicação entre Agentes

## O que e
Padrões e linguagens para agentes de IA trocarem informações de forma estruturada e eficiente.

## Protocolos
- FIPA-ACL (Foundation for Intelligent Physical Agents): Padrão clássico
- KQML (Knowledge Query and Manipulation Language)
- JSON-RPC ou gRPC para comunicação moderna entre microserviços de agentes

## Padrões de Mensagem
- Performativos: INFORM, REQUEST, PROPOSE, REFUSE
- Conteúdo: Ontologias compartilhadas (OWL, RDF) para significado comum
- Metadados: ID da mensagem, remetente, destinatário, timestamp

## Implementação
- Message brokers (RabbitMQ, Kafka) para comunicação assíncrona
- Service mesh (Istio) para roteamento e observabilidade
