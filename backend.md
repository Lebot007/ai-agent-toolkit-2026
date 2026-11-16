# Backend Development

Tudo sobre desenvolvimento backend: linguagens, frameworks, databases, APIs, arquitetura e mais.

## Linguagens e Frameworks

### Node.js
- Express: expressjs.com (minimalista)
- Fastify: fastify.io (performance)
- NestJS: nestjs.com (enterprise)
- Hono: hono.dev (edge-first, ultra-fast)

### Python
- FastAPI: fastapi.tiangolo.com (async, automatic docs)
- Django: djangoproject.com (batteries-included)
- Flask: flask.palletsprojects.com (microframework)

### Go
- Gin: gin-gonic.com (fast, minimal)
- Echo: echo.labstack.com (high performance)
- Fiber: gofiber.io (Express-inspired)

### Rust
- Actix Web: actix.rs (actor-based)
- Axum: github.com/tokio-rs/axum
- Rocket: rocket.rs (type-safe)

### Java
- Spring Boot: spring.io/projects/spring-boot
- Quarkus: quarkus.io (Kubernetes-native)

## Databases

### Relational
- PostgreSQL: postgresql.org
- MySQL: mysql.com
- SQLite: sqlite.org (embedded)
- CockroachDB: cockroachlabs.com (distributed SQL)

### NoSQL
- MongoDB: mongodb.com (document)
- Redis: redis.io (in-memory, cache)
- Cassandra: cassandra.apache.org (wide-column)
- DynamoDB: aws.amazon.com/dynamodb

### Search
- Elasticsearch: elastic.co
- Meilisearch: meilisearch.com (fast)
- Typesense: typesense.org (typo-tolerant)

## ORMs

### Node.js
- Prisma: prisma.io (type-safe)
- TypeORM: typeorm.io
- Drizzle: orm.drizzle.team
- Knex: knexjs.org (query builder)

### Python
- SQLAlchemy: sqlalchemy.org
- Django ORM: built-in
- Tortoise: tortoise.github.io (async)

### Go
- GORM: gorm.io
- sqlx: github.com/jmoiron/sqlx
- Ent: entgo.io (code generation)

## APIs

### REST
- OpenAPI/Swagger: swagger.io
- Best practices: resource naming, HTTP methods
- Pagination: cursor-based, offset-based

### GraphQL
- Apollo Server: apollographql.com
- GraphQL Yoga: the-guild.dev

### gRPC
- grpc.io: high-performance RPC
- Protocol Buffers: serialization

## Message Queues

- RabbitMQ: rabbitmq.com (AMQP)
- Apache Kafka: kafka.apache.org (event streaming)
- Redis Streams: redis.io
- NATS: nats.io (cloud-native)

## Authentication

- JWT: jsonwebtoken (stateless)
- OAuth 2.0: authorization framework
- OpenID Connect: identity layer
- Passkeys: webauthn (passwordless)

### Providers
- Auth0: auth0.com
- Clerk: clerk.com
- Supabase Auth: supabase.com

## Containers

### Docker
- Dockerfile: multi-stage builds
- docker-compose: multi-container
- Best practices: small images, non-root

### Kubernetes
- Pods, Deployments, Services
- Helm: package manager
- Ingress: routing

## CI/CD

- GitHub Actions: github.com/features/actions
- GitLab CI: gitlab.com
- ArgoCD: argoproj.github.io/cd (GitOps)

## Monitoring

- Prometheus: prometheus.io (metrics)
- Grafana: grafana.com (dashboards)
- ELK Stack: logging
- OpenTelemetry: opentelemetry.io

## Arquitetura

### Patterns
- Microservices: servicos independentes
- Monolith: single codebase
- Serverless: AWS Lambda, Cloudflare Workers
- Event-driven: message queues
- CQRS: Command Query Responsibility Segregation

### Design Principles
- SOLID: Single responsibility, Open-closed, Liskov, Interface segregation, Dependency inversion
- DRY: Don't Repeat Yourself
- KISS: Keep It Simple, Stupid

## Seguranca

- OWASP Top 10: injection, broken auth, XSS
- Rate limiting: prevenir abuse
- Input validation: nunca confiar em user input
- HTTPS everywhere
- Secrets management: HashiCorp Vault

## Recursos
- The Twelve-Factor App
- Martin Fowler's Blog
- System Design Primer