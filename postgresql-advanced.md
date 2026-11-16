# PostgreSQL Avancado - Tecnicas Avancadas

## O que e
Sistema de banco de dados relacional open-source avancado.

## Features Avancadas

### JSONB
CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    name TEXT,
    attributes JSONB
);

INSERT INTO products (name, attributes) VALUES
('Laptop', '{"brand": "Dell", "specs": {"cpu": "i7", "ram": 16}}');

-- Query JSONB
SELECT name, attributes->>'brand' as brand
FROM products
WHERE attributes->'specs'->>'cpu' = 'i7';

-- Index JSONB
CREATE INDEX idx_product_attrs ON products USING GIN (attributes);

### Arrays
CREATE TABLE articles (
    id SERIAL PRIMARY KEY,
    title TEXT,
    tags TEXT[]
);

INSERT INTO articles (title, tags) VALUES
('PostgreSQL Guide', '{database, sql, postgres}');

-- Query arrays
SELECT * FROM articles WHERE 'database' = ANY(tags);
SELECT * FROM articles WHERE tags @> '{sql, postgres}';

### HSTORE
CREATE EXTENSION hstore;

CREATE TABLE settings (
    id SERIAL PRIMARY KEY,
    config HSTORE
);

INSERT INTO settings (config) VALUES
('theme => dark, language => en'::hstore);

-- Query hstore
SELECT config->'theme' FROM settings;

## Window Functions

### Exemplo Completo
SELECT 
    employee_id,
    department,
    salary,
    ROW_NUMBER() OVER w as row_num,
    RANK() OVER w as rank,
    DENSE_RANK() OVER w as dense_rank,
    LAG(salary, 1) OVER w as prev_salary,
    LEAD(salary, 1) OVER w as next_salary,
    AVG(salary) OVER (PARTITION BY department) as dept_avg,
    SUM(salary) OVER (ORDER BY salary ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) as running_total
FROM employees
WINDOW w AS (PARTITION BY department ORDER BY salary DESC);

## CTEs Recursivas

### Hierarquia de Organizacoes
WITH RECURSIVE org_tree AS (
    -- Base: root nodes
    SELECT id, name, parent_id, 1 as level, ARRAY[id] as path
    FROM organizations
    WHERE parent_id IS NULL
    
    UNION ALL
    
    -- Recursive: children
    SELECT o.id, o.name, o.parent_id, ot.level + 1, ot.path || o.id
    FROM organizations o
    INNER JOIN org_tree ot ON o.parent_id = ot.id
)
SELECT * FROM org_tree ORDER BY path;

## Performance

### EXPLAIN ANALYZE
EXPLAIN (ANALYZE, BUFFERS, FORMAT TEXT)
SELECT * FROM orders WHERE customer_id = 123;

### Indexes Avancados
-- Partial index
CREATE INDEX idx_active_users ON users(email) WHERE active = true;

-- Expression index
CREATE INDEX idx_lower_email ON users(LOWER(email));

-- Composite index
CREATE INDEX idx_composite ON orders(customer_id, order_date);

-- GIN index for full-text search
CREATE INDEX idx_search ON articles USING GIN(to_tsvector('english', content));

### Partitioning
CREATE TABLE logs (
    id SERIAL,
    created_at TIMESTAMP,
    message TEXT
) PARTITION BY RANGE (created_at);

CREATE TABLE logs_2024_q1 PARTITION OF logs
FOR VALUES FROM ('2024-01-01') TO ('2024-04-01');

### Vacuum e Analyze
VACUUM ANALYZE orders;
VACUUM FULL orders;  # Reclaim space

## Extensions

### PostGIS (Geospatial)
CREATE EXTENSION postgis;

CREATE TABLE locations (
    id SERIAL PRIMARY KEY,
    name TEXT,
    geom GEOMETRY(POINT, 4326)
);

-- Find nearby locations
SELECT name
FROM locations
WHERE ST_DWithin(geom, ST_MakePoint(-73.9857, 40.7484, 4326), 1000);

### pg_trgm (Fuzzy Search)
CREATE EXTENSION pg_trgm;

CREATE INDEX idx_trgm ON users USING GIN (name gin_trgm_ops);

-- Fuzzy search
SELECT * FROM users WHERE name % 'Jonh';  -- typo for John

## Replication e HA

### Streaming Replication
-- Primary (postgresql.conf)
wal_level = replica
max_wal_senders = 3
wal_keep_size = 64

-- Standby
pg_basebackup -h primary_host -D /var/lib/postgresql/data -U replicator -P

### Logical Replication
-- Publisher
CREATE PUBLICATION my_pub FOR TABLE users, orders;

-- Subscriber
CREATE SUBSCRIPTION my_sub CONNECTION 'host=primary dbname=mydb' PUBLICATION my_pub;

## Best Practices

### Schema Design
- Usar tipos apropriados
- Normalizar quando apropriado
- Usar constraints
- Documentar com comments

### Performance
- Analisar query plans
- Criar indexes estrategicos
- Usar connection pooling (pgBouncer)
- Monitorar com pg_stat_statements

### Backup
- pg_dump para logical backups
- pg_basebackup para physical backups
- Testar restores regularmente

## Quando Usar
- Aplicacoes que precisam de features avancadas
- JSONB para dados semi-estruturados
- Full-text search
- Geospatial data
- Ambientes que precisam de extensibilidade