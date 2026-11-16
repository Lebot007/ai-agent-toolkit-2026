# SQL Avancado - Tecnicas Avancadas de SQL

## O que e
Tecnicas avancadas para escrever queries SQL eficientes e poderosas.

## Window Functions

### ROW_NUMBER
SELECT 
    employee_id,
    department,
    salary,
    ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) as rank
FROM employees;

### RANK e DENSE_RANK
SELECT 
    name,
    score,
    RANK() OVER (ORDER BY score DESC) as rank,
    DENSE_RANK() OVER (ORDER BY score DESC) as dense_rank
FROM students;

### LAG e LEAD
SELECT 
    date,
    sales,
    LAG(sales, 1) OVER (ORDER BY date) as prev_day_sales,
    LEAD(sales, 1) OVER (ORDER BY date) as next_day_sales
FROM daily_sales;

### Running Totals
SELECT 
    date,
    amount,
    SUM(amount) OVER (ORDER BY date) as running_total
FROM transactions;

## Common Table Expressions (CTEs)

### CTE Basico
WITH high_earners AS (
    SELECT employee_id, name, salary
    FROM employees
    WHERE salary > 100000
)
SELECT * FROM high_earners;

### CTE Recursivo
WITH RECURSIVE org_chart AS (
    -- Base case: top-level managers
    SELECT employee_id, name, manager_id, 1 as level
    FROM employees
    WHERE manager_id IS NULL
    
    UNION ALL
    
    -- Recursive case: employees under managers
    SELECT e.employee_id, e.name, e.manager_id, oc.level + 1
    FROM employees e
    INNER JOIN org_chart oc ON e.manager_id = oc.employee_id
)
SELECT * FROM org_chart ORDER BY level, name;

## Subqueries

### Correlated Subquery
SELECT 
    e.name,
    e.salary,
    (SELECT AVG(salary) FROM employees WHERE department = e.department) as dept_avg
FROM employees e;

### EXISTS
SELECT name
FROM customers c
WHERE EXISTS (
    SELECT 1 FROM orders o WHERE o.customer_id = c.id
);

## Joins Avancados

### Self Join
SELECT 
    e1.name as employee,
    e2.name as manager
FROM employees e1
LEFT JOIN employees e2 ON e1.manager_id = e2.id;

### Cross Join
SELECT 
    p.name as product,
    s.name as store
FROM products p
CROSS JOIN stores s;

## Aggregate Functions Avancadas

### GROUPING SETS
SELECT 
    department,
    position,
    COUNT(*) as count
FROM employees
GROUP BY GROUPING SETS (
    (department, position),
    (department),
    ()
);

### ROLLUP
SELECT 
    region,
    country,
    SUM(sales) as total_sales
FROM sales_data
GROUP BY ROLLUP (region, country);

### CUBE
SELECT 
    product,
    region,
    SUM(sales)
FROM sales_data
GROUP BY CUBE (product, region);

## Performance

### EXPLAIN ANALYZE
EXPLAIN ANALYZE
SELECT * FROM orders WHERE customer_id = 123;

### Indexes
CREATE INDEX idx_customer_id ON orders(customer_id);
CREATE INDEX idx_composite ON orders(customer_id, order_date);

### Partitioning
CREATE TABLE sales (
    id SERIAL,
    sale_date DATE,
    amount DECIMAL
) PARTITION BY RANGE (sale_date);

CREATE TABLE sales_2024 PARTITION OF sales
FOR VALUES FROM ('2024-01-01') TO ('2025-01-01');

## Best Practices

### Query Writing
- Usar CTEs para legibilidade
- Evitar SELECT *
- Usar aliases claros
- Comentar queries complexas

### Performance
- Analisar execution plans
- Criar indexes apropriados
- Evitar funcoes em WHERE
- Usar EXISTS ao inves de IN quando apropriado

### Manutencao
- Documentar queries complexas
- Versionar schemas
- Monitorar query performance

## Quando Usar
- Relatorios complexos
- Analise de dados
- ETL processes
- Data warehousing