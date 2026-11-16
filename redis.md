# Redis - In-Memory Data Store

Conhecimento tecnico completo sobre Redis: modelagem, cache, busca, clustering, seguranca e observabilidade.

## O que e Redis

Banco de dados in-memory, chave-valor, com suporte a estruturas de dados ricas.

## Estruturas de Dados

### Strings
- SET, GET, MSET, MGET
- INCR, DECR, INCRBY
- EXPIRE, TTL (time-to-live)
- SETEX (set with expiration)

### Hashes
- HSET, HGET, HMSET, HMGET
- HGETALL, HKEYS, HVALS
- HINCRBY, HDEL
- Ideal para: objetos, user profiles

### Lists
- LPUSH, RPUSH, LPOP, RPOP
- LRANGE, LLEN
- BLPOP, BRPOP (blocking)
- Ideal para: filas, timelines, logs

### Sets
- SADD, SREM, SMEMBERS
- SISMEMBER, SCARD
- SUNION, SINTER, SDIFF
- Ideal para: tags, unique collections

### Sorted Sets
- ZADD, ZREM, ZSCORE
- ZRANGE, ZRANGEBYSCORE
- ZRANK, ZREVRANK
- Ideal para: leaderboards, ranking

### Bitmaps
- SETBIT, GETBIT, BITCOUNT
- BITOP (AND, OR, XOR)
- Ideal para: presence tracking, A/B tests

### HyperLogLog
- PFADD, PFCOUNT
- Aproximacao de cardinalidade
- Ideal para: unique visitors

### Streams
- XADD, XREAD, XRANGE
- XACK, XPENDING
- Ideal para: event sourcing, message queues

### Geospatial
- GEOADD, GEODIST
- GEORADIUS, GEOSEARCH
- Ideal para: location-based services

## Padroes de Uso

### Cache
- Cache-aside (lazy loading)
- Write-through
- Write-behind
- TTL strategies

### Session Store
- User sessions
- JWT blacklists
- Shopping carts

### Message Queue
- Lists como filas
- Streams para event sourcing
- Pub/Sub para broadcasting

### Rate Limiting
- Fixed window
- Sliding window
- Token bucket
- Leaky bucket

### Distributed Locks
- SETNX (set if not exists)
- Redlock algorithm
- Timeout handling

### Leaderboards
- Sorted sets com scores
- ZREVRANGE para top N
- ZRANK para ranking

## Modelagem de Dados

### Key Naming Convention
- user:123 (user ID 123)
- user:123:profile
- user:123:sessions
- post:456:comments
- session:abc123

### Namespacing
- Usar dois pontos como separador
- Prefixos por dominio
- Evitar keys muito longas

### Expiration Strategy
- TTL curto para cache
- TTL longo para sessions
- Sem TTL para dados persistentes
- Monitor memory usage

## Performance

### Otimizacoes
- Pipeline commands (reduzir round trips)
- Use MULTI/EXEC para transactions
- Evitar KEYS * (usar SCAN)
- Use connection pooling
- Enable compression para values grandes

### Memory Management
- maxmemory-policy: allkeys-lru, volatile-lru
- Monitor fragmentation ratio
- Use MEMORY USAGE para analisar keys
- Consider Redis Cluster para scale

### Benchmarks
- Single instance: ~100k ops/sec
- Pipeline: ~500k ops/sec
- Cluster: linear scale

## Clustering

### Redis Cluster
- Automatic sharding
- 16384 hash slots
- Master-replica replication
- Automatic failover

### Redis Sentinel
- High availability
- Automatic failover
- Monitoring
- Configuration provider

## Seguranca

### Authentication
- requirepass no redis.conf
- ACL (Access Control Lists)
- Command renaming

### Network
- Bind to specific IPs
- Protected mode
- TLS encryption
- Firewall rules

### Data Protection
- Disable dangerous commands (FLUSHALL, CONFIG)
- Use ACLs para restrict acesso
- Audit logging

## Observabilidade

### Metrics
- connected_clients
- used_memory
- keyspace_hits/misses
- ops_per_sec
- instantaneous_ops_per_sec

### Monitoring Tools
- INFO command
- MONITOR (debug only)
- SLOWLOG
- Redis Exporter + Prometheus

### Alerting
- Memory usage > 80%
- Hit ratio < 90%
- High latency
- Connection spikes

## Persistencia

### RDB (Snapshots)
- Point-in-time snapshots
- Compacto, bom para backup
- Perda de dados entre snapshots

### AOF (Append-Only File)
- Log de todas as operacoes
- Mais duravel
- Maior tamanho de arquivo

### Hibrido
- RDB + AOF
- Best of both worlds

## Casos de Uso

- Caching layer
- Session management
- Real-time analytics
- Rate limiting
- Message queues
- Leaderboards
- Geospatial services
- Pub/Sub

## Recursos
- Redis Documentation: redis.io/docs
- Redis University: university.redis.com
- Redis GitHub: github.com/redis/redis