# Query Optimization - Otimizacao de Queries

## O que e
Tecnicas para escrever queries SQL eficientes e rapidas.

## Analise de Performance

### EXPLAIN
EXPLAIN SELECT * FROM orders WHERE customer_id = 123;

-- Com ANALYZE (executa a query)
EXPLAIN ANALYZE SELECT * FROM orders WHERE customer_id = 123;

-- PostgreSQL: com BUFFERS
EXPLAIN (ANALYZE, BUFFERS) SELECT * FROM orders WHERE customer_id = 123;

### Interpretar EXPLAIN
- Sequential Scan: le toda tabela (ruim para tabelas grandes)
- Index Scan: usa index (bom)
- Index Only Scan: melhor ainda
- Bitmap Heap Scan: usa bitmap index

## Indexes

### Quando Criar Index
- Colunas em WHERE frequentemente
- Colunas em JOIN
- Colunas em ORDER BY
- Colunas com alta seletividade

### Tipos de Index

#### B-Tree (default)
CREATE INDEX idx_orders_customer ON orders(customer_id);

#### Composite Index
CREATE INDEX idx_orders_cust_date ON orders(customer_id, order_date);
-- Ordem importa! (customer_id, order_date) != (order_date, customer_id)

#### Partial Index
CREATE INDEX idx_active_orders ON orders(customer_id)
WHERE status = 'active';

#### Expression Index
CREATE INDEX idx_lower_email ON users(LOWER(email));

#### GIN (para arrays, JSONB, full-text)
CREATE INDEX idx_tags ON products USING GIN(tags);

#### BRIN (para dados ordenados)
CREATE INDEX idx_created_brin ON logs USING BRIN(created_at);

### Index Maintenance
-- PostgreSQL
REINDEX INDEX idx_orders_customer;
VACUUM ANALYZE orders;

-- Verificar indexes nao usados
SELECT * FROM pg_stat_user_indexes
WHERE idx_scan = 0;

## Otimizacoes Comuns

### Evitar SELECT *
-- Ruim
SELECT * FROM orders;

-- Bom
SELECT id, customer_id, order_date, total
FROM orders;

### Usar EXISTS ao inves de IN
-- Mais lento (para subqueries grandes)
SELECT * FROM customers
WHERE id IN (SELECT customer_id FROM orders);

-- Mais rapido
SELECT * FROM customers c
WHERE EXISTS (SELECT 1 FROM orders o WHERE o.customer_id = c.id);

### Evitar Funcoes em WHERE
-- Ruim (nao usa index)
SELECT * FROM users WHERE YEAR(created_at) = 2024;

-- Bom (usa index)
SELECT * FROM users
WHERE created_at >= '2024-01-01' AND created_at < '2025-01-01';

### LIMIT e OFFSET
-- Ruim para paginacao (OFFSET 1000000 e lento)
SELECT * FROM orders ORDER BY id LIMIT 10 OFFSET 1000000;

-- Bom (keyset pagination)
SELECT * FROM orders
WHERE id > 1000000
ORDER BY id
LIMIT 10;

### JOINs
-- Usar INNER JOIN quando possivel (mais rapido que LEFT JOIN)
SELECT o.*, c.name
FROM orders o
INNER JOIN customers c ON o.customer_id = c.id;

-- Evitar cartesian products
-- Ruim:
SELECT * FROM orders, customers;  -- N * M rows

-- Bom:
SELECT * FROM orders o
INNER JOIN customers c ON o.customer_id = c.id;

### Subqueries vs JOINs
-- Subquery
SELECT name,
       (SELECT COUNT(*) FROM orders WHERE customer_id = c.id) as order_count
FROM customers c;

-- JOIN (geralmente mais rapido)
SELECT c.name, COUNT(o.id) as order_count
FROM customers c
LEFT JOIN orders o ON c.id = o.customer_id
GROUP BY c.id, c.name;

## Partitioning

### Range Partitioning
CREATE TABLE sales (
    id SERIAL,
    sale_date DATE,
    amount DECIMAL
) PARTITION BY RANGE (sale_date);

CREATE TABLE sales_2024 PARTITION OF sales
FOR VALUES FROM ('2024-01-01') TO ('2025-01-01');

### List Partitioning
CREATE TABLE logs (
    id SERIAL,
    level TEXT,
    message TEXT
) PARTITION BY LIST (level);

CREATE TABLE logs_error PARTITION OF logs
FOR VALUES IN ('ERROR', 'CRITICAL');

## Query Patterns

### Top-N por Grupo
-- Top 3 produtos por categoria
WITH ranked AS (
    SELECT *,
           ROW_NUMBER() OVER (PARTITION BY category ORDER BY sales DESC) as rn
    FROM products
)
SELECT * FROM ranked WHERE rn <= 3;

### Running Total
SELECT 
    date,
    amount,
    SUM(amount) OVER (ORDER BY date) as running_total
FROM transactions;

### Deduplicacao
DELETE FROM products
WHERE id NOT IN (
    SELECT MIN(id)
    FROM products
    GROUP BY sku
);

## Monitoring

### Slow Query Log
-- PostgreSQL
ALTER SYSTEM SET log_min_duration_statement = 1000;  -- 1 second
SELECT pg_reload_conf();

-- MySQL
SET GLOBAL slow_query_log = 'ON';
SET GLOBAL long_query_time = 1;

### Query Stats
-- PostgreSQL: pg_stat_statements
CREATE EXTENSION pg_stat_statements;

SELECT query, calls, total_time, mean_time
FROM pg_stat_statements
ORDER BY mean_time DESC
LIMIT 10;

## Best Practices

### Design
- Normalizar quando apropriado
- Desnormalizar para performance (com cuidado)
- Usar tipos de dados apropriados
- Definir constraints

### Indexing
- Nao criar indexes demais (overhead de escrita)
- Monitorar uso de indexes
- Remover indexes nao usados
- Considerar composite indexes

### Queries
- Sempre usar EXPLAIN
- Evitar SELECT *
- Usar pagination
- Cache quando apropriado

### Maintenance
- VACUUM regularmente (PostgreSQL)
- Atualizar estatisticas (ANALYZE)
- Rebuild indexes periodicamente

## Trade-offs
- Read vs Write performance
- Index size vs query speed
- Normalization vs denormalization

## Quando Otimizar
- Queries lentas (>1s)
- Alto load no banco
- Timeout de aplicacao
- Scaling issues