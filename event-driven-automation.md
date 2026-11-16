# Event-Driven Automation - Automação Orientada a Eventos

## O que e
Sistemas onde ações de automação são disparadas automaticamente por eventos específicos, sem polling ou intervenção manual.

## Arquitetura
- Event Producers: Aplicações que emitem eventos (ex: "novo pedido criado", "arquivo enviado")
- Event Bus: Kafka, RabbitMQ, ou AWS EventBridge para roteamento
- Event Consumers: Agentes ou funções serverless que processam o evento e executam a ação

## Padrões
- Pub/Sub: Múltiplos consumidores podem reagir ao mesmo evento
- Event Sourcing: Estado do sistema é reconstruído a partir do log de eventos
- Saga Pattern: Gerenciar transações distribuídas através de eventos de compensação

## Casos de Uso
- Notificar equipe de vendas automaticamente quando um lead de alto valor se cadastra
- Acionar pipeline de limpeza de dados assim que um novo arquivo chega no S3
