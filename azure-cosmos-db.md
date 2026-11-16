# Azure Cosmos DB

Boas praticas de bancos NoSQL, modelagem, consultas, indexacao, desempenho e seguranca.

## O que e Cosmos DB

Banco de dados NoSQL multi-modelo, globalmente distribuido, da Microsoft Azure.

## APIs Suportadas

### NoSQL (Core)
- Document-oriented
- JSON nativo
- SQL-like queries

### MongoDB
- Compativel com MongoDB API
- Wire protocol support
- Migration facilitada

### Cassandra
- Wide-column store
- CQL (Cassandra Query Language)

### Gremlin
- Graph database
- Property graph model
- Traversals

### Table
- Key-value store
- Azure Table Storage compativel

## Modelagem de Dados

### Principios
- Denormalizacao e comum (evitar joins)
- Duplicacao de dados e aceitavel
- Design baseado em query patterns
- Partition key e crucial

### Partition Key
- Escolha com cuidado (nao pode mudar)
- Alto cardinalidade
- Distribui dados uniformemente
- Impacta performance e custo

### Padroes Comuns

#### One-to-Few
- Embed child documents
- Exemplo: user com addresses

#### One-to-Many
- Reference com foreign key
- Exemplo: user com orders

#### One-to-Few-Thousands
- Separate containers
- Exemplo: user com posts

#### One-to-Squillions
- Separate containers com partition
- Exemplo: user com log entries

## Consultas

### SQL API

SELECT * FROM c
SELECT c.id, c.name FROM c WHERE c.age > 18
SELECT VALUE c.name FROM c
SELECT * FROM c ORDER BY c.created_at DESC
SELECT * FROM c OFFSET 10 LIMIT 20

### Agregacoes
- COUNT, SUM, AVG, MIN, MAX
- GROUP BY
- ARRAY_LENGTH

### Funcoes
- String: CONCAT, SUBSTRING, LOWER, UPPER
- Math: CEILING, FLOOR, ROUND
- Date: GetCurrentDateTime, DateTimeAdd
- Array: ARRAY_CONTAINS, ARRAY_LENGTH

### Stored Procedures
- Executam no servidor
- Transacoes atomicas
- Reduzem round trips

## Indexacao

### Automatic Indexing
- Todos os campos indexados por default
- Index path policies

### Index Types
- **Range:** para ORDER BY, filtros
- **Spatial:** para geospatial queries
- **Composite:** para multi-field ORDER BY

### Otimizacao
- Excluir campos nao usados em queries
- Incluir apenas campos necessarios
- Monitor RU consumption

## Desempenho

### Request Units (RU)
- Unidade de medida de custo
- Operacoes tem custo em RU
- Provisioned throughput vs serverless

### Otimizacoes
- Point reads (id + partition key) sao mais baratos
- Evitar cross-partition queries
- Use continuation tokens para paginacao
- Cache responses quando possivel
- Connection pooling

### Monitoring
- Azure Monitor
- Metrics: RU consumption, latency, errors
- Query execution plans
- Diagnostic logs

## Consistencia

### 5 Niveis
1. **Strong:** linearizability, mais lento
2. **Bounded Staleness:** lag limitado
3. **Session:** consistencia por session
4. **Consistent Prefix:** sem out-of-order
5. **Eventual:** mais rapido, menos garantias

### Escolha
- Strong: financeiro, inventario
- Session: user-specific data
- Eventual: feeds, analytics

## Seguranca

### Authentication
- Azure AD integration
- Resource tokens
- Master keys

### Authorization
- Role-based access control (RBAC)
- Data encryption at rest
- Data encryption in transit (TLS)

### Network
- Private endpoints
- Virtual network integration
- Firewall rules

### Compliance
- SOC, ISO, HIPAA, GDPR
- Customer-managed keys
- Audit logging

## Multi-Region

### Global Distribution
- Replicacao automatica
- Multiple write regions
- Automatic failover

### Use Cases
- Low latency global
- Disaster recovery
- Read scalability

## Casos de Uso

- E-commerce catalogs
- User profiles
- IoT telemetry
- Gaming leaderboards
- Social feeds
- Real-time analytics

## Recursos
- Azure Cosmos DB Documentation
- Microsoft Learn paths
- GitHub samples