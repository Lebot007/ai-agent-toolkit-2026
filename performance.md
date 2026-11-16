# Performance e Desempenho

Otimizacao de velocidade, desempenho, profiling, caching e tecnicas para sistemas de alta performance.

## Profiling

### Python
- **cProfile:** built-in profiler
- **py-spy:** github.com/benfred/py-spy (sampling profiler)
- **memory_profiler:** github.com/pythonprofilers/memory_profiler
- **line_profiler:** github.com/pyutils/line_profiler

### Node.js
- **Chrome DevTools:** CPU profiling, memory snapshots
- **clinic.js:** clinicjs.org (performance diagnostics)
- **0x:** github.com/davidmarkclements/0x (flamegraphs)

### Go
- **pprof:** pkg/runtime/pprof (CPU, memory, goroutines)
- **trace:** runtime/trace (execution trace)

### Rust
- **perf:** linux perf tools
- **flamegraph:** github.com/flamegraph-rs/flamegraph
- **criterion:** github.com/bheisler/criterion.rs (benchmarks)

### Java
- **VisualVM:** visualvm.github.io
- **JProfiler:** ej-technologies.com/jprofiler
- **Async Profiler:** github.com/async-profiler/async-profiler

## Benchmarking

### Micro-benchmarks
- **Python:** timeit, pytest-benchmark
- **Node.js:** benchmark.js
- **Go:** testing.B
- **Rust:** criterion
- **Java:** JMH (Java Microbenchmark Harness)

### Load Testing
- **k6:** k6.io (JavaScript-based)
- **Locust:** locust.io (Python-based)
- **Apache JMeter:** jmeter.apache.org
- **Vegeta:** github.com/tsenart/vegeta (Go)

## Caching Strategies

### Application Cache
- **Redis:** in-memory data store
- **Memcached:** memcached.org
- **In-memory:** application-level (Map, LRU cache)

### HTTP Cache
- **Cache-Control:** max-age, s-maxage, no-cache
- **ETag:** entity tags
- **Last-Modified:** conditional requests
- **CDN:** Cloudflare, AWS CloudFront, Fastly

### Database Cache
- **Query cache:** MySQL query cache (deprecated)
- **Materialized views:** PostgreSQL, Oracle
- **Read replicas:** distribute read load

### Patterns
- **Cache-aside:** lazy loading
- **Write-through:** write to cache and DB
- **Write-behind:** async write to DB
- **Refresh-ahead:** proactively refresh

## Otimizacoes de Algoritmos

### Complexidade
- Big O notation: O(1), O(log n), O(n), O(n log n), O(n^2)
- Evitar nested loops quando possivel
- Use hash tables para O(1) lookups
- Sorting: O(n log n) vs O(n^2)

### Data Structures
- **Arrays:** O(1) access, O(n) search
- **Hash Maps:** O(1) lookup, insert, delete
- **Trees:** O(log n) search, insert, delete
- **Graphs:** BFS, DFS, Dijkstra

### Techniques
- **Memoization:** cache expensive function calls
- **Dynamic programming:** overlapping subproblems
- **Greedy algorithms:** local optimal choices
- **Divide and conquer:** split, solve, combine

## Database Performance

### Indexing
- B-tree indexes: range queries
- Hash indexes: equality
- Composite indexes: multi-column
- Covering indexes: avoid table lookups

### Query Optimization
- EXPLAIN ANALYZE (PostgreSQL)
- Avoid SELECT *
- Use appropriate JOINs
- Limit result sets
- Avoid N+1 queries

### Connection Pooling
- **PgBouncer:** pgbouncer.org (PostgreSQL)
- **HikariCP:** github.com/brettwooldridge/HikariCP (Java)
- **node-postgres:** built-in pooling

## Concurrency e Parallelism

### Async/Await
- **Python:** asyncio, aiohttp
- **Node.js:** Promises, async/await
- **Rust:** tokio, async-std

### Threading
- **Python:** threading, multiprocessing, concurrent.futures
- **Java:** ExecutorService, CompletableFuture
- **Go:** goroutines, channels

### Message Queues
- **RabbitMQ:** rabbitmq.com
- **Apache Kafka:** kafka.apache.org
- **Redis Streams:** redis.io

## Network Performance

### HTTP/2 e HTTP/3
- Multiplexing
- Header compression
- Server push
- QUIC protocol (HTTP/3)

### Compression
- **gzip:** universal
- **Brotli:** better compression (Google)
- **zstd:** fast compression (Facebook)

### CDN
- Edge caching
- Load balancing
- DDoS protection

## Frontend Performance

### Core Web Vitals
- **LCP:** Largest Contentful Paint (< 2.5s)
- **FID:** First Input Delay (< 100ms)
- **CLS:** Cumulative Layout Shift (< 0.1)

### Otimizacoes
- Code splitting
- Lazy loading
- Image optimization (WebP, AVIF)
- Font optimization
- Service Workers

## Recursos
- High Performance Web Sites (Steve Souders)
- Systems Performance (Brendan Gregg)
- Google Web Fundamentals: web.dev