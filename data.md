# Data Analytics

Skill completo para analise de dados, metricas, indicadores, relatorios, dashboards e inteligencia de negocios.

## Ferramentas de Analise

### Python Libraries
- **Pandas:** manipulacao e analise de dados tabulares
- **NumPy:** computacao numerica e arrays
- **Polars:** alternativa rapida ao Pandas (Rust-based)
- **DuckDB:** banco analitico embarcado
- **Vaex:** big data em memoria (out-of-core)

### Visualizacao
- **Matplotlib:** plots basicos e customizaveis
- **Seaborn:** visualizacao estatistica
- **Plotly:** graficos interativos
- **Altair:** declarative statistical visualization
- **Bokeh:** visualizacao interativa para web

### BI Tools
- **Metabase:** open-source BI
- **Apache Superset:** enterprise BI
- **Grafana:** monitoring e dashboards
- **Redash:** query e visualize SQL
- **Lightdash:** dbt-native BI

## Metricas e KPIs

### Definicao
- **Metric:** medida quantitativa (ex: usuarios ativos)
- **KPI:** metric atrelada a objetivo estrategico
- **Leading indicators:** predizem resultados futuros
- **Lagging indicators:** medem resultados passados

### Tipos de Metricas
- **Absolutas:** contagem simples (ex: 1000 usuarios)
- **Razoes:** proporcoes (ex: 5% churn rate)
- **Taxas:** por unidade de tempo (ex: 10 vendas/dia)
- **Indices:** normalizados (ex: NPS = 45)

### Frameworks
- **AARRR:** Acquisition, Activation, Retention, Revenue, Referral
- **HEART:** Happiness, Engagement, Adoption, Retention, Task success
- **OKRs:** Objectives and Key Results
- **North Star Metric:** unica metric que melhor representa valor

## Analise Estatistica

### Descritiva
- Media, mediana, moda
- Desvio padrao, variancia
- Quartis, percentis
- Distribuicoes (normal, binomial, Poisson)

### Inferencial
- Testes de hipotese (t-test, chi-square, ANOVA)
- Intervalos de confianca
- Regressao (linear, logistica, polinomial)
- Correlacao (Pearson, Spearman)

### Avancada
- Series temporais (ARIMA, Prophet)
- Clusterizacao (K-means, DBSCAN)
- Reducao de dimensionalidade (PCA, t-SNE)
- Survival analysis

## Dashboards

### Principios de Design
- Hierarquia visual clara
- Menos e mais (evitar clutter)
- Consistencia de cores e tipografia
- Interatividade util (filtros, drill-down)
- Responsividade (mobile, desktop)

### Componentes Essenciais
- KPIs no topo (big numbers)
- Graficos de tendencia (line charts)
- Comparacoes (bar charts)
- Distribuicoes (histograms, box plots)
- Filtros globais

## SQL para Analise

### Queries Essenciais
- Agregacoes (COUNT, SUM, AVG, MIN, MAX)
- Grouping (GROUP BY, HAVING)
- Window functions (ROW_NUMBER, RANK, LAG, LEAD)
- CTEs (Common Table Expressions)
- Joins (INNER, LEFT, RIGHT, FULL)

### Otimizacao
- Indices em colunas de WHERE/JOIN
- Partitioning por data
- Materialized views
- Query execution plans
- Avoiding SELECT *

## Data Pipelines

### ETL vs ELT
- **ETL:** Extract, Transform, Load (tradicional)
- **ELT:** Extract, Load, Transform (moderno, cloud)

### Ferramentas
- **Airflow:** orquestracao de workflows
- **dbt:** transformacoes SQL-based
- **Prefect:** workflows Python-native
- **Dagster:** data orchestration
- **Mage:** hybrid ETL/ELT

## Recursos
- Pandas documentation
- dbt documentation
- Apache Superset docs
- Metabase documentation