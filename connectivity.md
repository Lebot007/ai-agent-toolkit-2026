# Conectividade e Integracoes

Webhooks, event streaming, message brokers, real-time, APIs de integracao e patterns de comunicacao.

## Webhooks

### O que sao
- HTTP callbacks
- Event-driven notifications
- Push vs pull

### Implementacao
- Endpoint publico (HTTPS)
- Signature verification (HMAC)
- Retry logic (exponential backoff)
- Idempotency

### Providers
- **GitHub Webhooks:** github.com
- **Stripe Webhooks:** stripe.com
- **Slack Events:** slack.com
- **Twilio:** twilio.com

### Ferramentas
- **ngrok:** ngrok.com (tunnel local para public)
- **webhook.site:** webhook.site (testing)
- **Hookdeck:** hookdeck.com (management)

## Message Brokers

### RabbitMQ
- **Site:** rabbitmq.com
- AMQP protocol
- Exchanges: direct, topic, fanout, headers
- Queues: durable, transient
- Use cases: task queues, pub/sub

### Apache Kafka
- **Site:** kafka.apache.org
- Distributed event streaming
- Topics, partitions, consumer groups
- High throughput, durability
- Use cases: event sourcing, log aggregation

### Redis Streams
- **Site:** redis.io
- Lightweight streaming
- Consumer groups
- Use cases: real-time feeds, chat

### NATS
- **Site:** nats.io
- Cloud-native messaging
- JetStream for persistence
- Low latency

### Amazon SQS
- **Site:** aws.amazon.com/sqs
- Managed message queue
- Standard vs FIFO queues
- Visibility timeout

## Real-Time Communication

### WebSockets
- **Socket.IO:** socket.io (JavaScript)
- **ws:** github.com/websockets/ws (Node.js)
- **Django Channels:** channels.readthedocs.io
- **FastAPI WebSockets:** built-in

### Server-Sent Events (SSE)
- Unidirectional (server to client)
- Simpler than WebSockets
- Auto-reconnect

### gRPC Streaming
- **grpc.io:** high-performance RPC
- Unary, server streaming, client streaming, bidirectional
- Protocol Buffers

### MQTT
- **Site:** mqtt.org
- IoT messaging protocol
- Pub/sub model
- QoS levels: 0, 1, 2

## Event-Driven Architecture

### Patterns
- **Event sourcing:** persist events, derive state
- **CQRS:** separate read and write models
- **Eventual consistency:** accept temporary inconsistency
- **Saga pattern:** distributed transactions

### Event Schema
- **CloudEvents:** cloudevents.io (standard)
- **JSON Schema:** json-schema.org
- **Protobuf:** Protocol Buffers
- **Avro:** avro.apache.org

### Event Stores
- **EventStoreDB:** eventstore.com
- **Kafka:** kafka.apache.org
- **Axon:** axoniq.io (Java)

## API Gateway

### Features
- Rate limiting
- Authentication
- Request routing
- Load balancing
- Monitoring

### Tools
- **Kong:** konghq.com (open-source)
- **Tyk:** tyk.io
- **AWS API Gateway:** aws.amazon.com/api-gateway
- **Cloudflare Workers:** cloudflare.com

## Service Mesh

### Istio
- **Site:** istio.io
- Traffic management
- Security (mTLS)
- Observability

### Linkerd
- **Site:** linkerd.io
- Lightweight
- Easy to deploy

## Integration Patterns

### Synchronous
- REST APIs
- gRPC
- GraphQL

### Asynchronous
- Message queues
- Event streaming
- Webhooks

### Hybrid
- Request-reply pattern
- Choreography vs orchestration

## Data Integration

### ETL/ELT
- **Airbyte:** airbyte.com (open-source)
- **Fivetran:** fivetran.com
- **dbt:** getdbt.com (transformations)
- **Apache NiFi:** nifi.apache.org

### CDC (Change Data Capture)
- **Debezium:** debezium.io (Kafka Connect)
- **Maxwell:** github.com/zendesk/maxwell (MySQL)
- **Oracle GoldenGate:** oracle.com

## Resources
- Enterprise Integration Patterns (Gregor Hohpe)
- Designing Event-Driven Systems (Ben Stopford)
- Martin Fowler's Blog