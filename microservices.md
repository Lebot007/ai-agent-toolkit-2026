# Microservices - Arquitetura de Microservicos

## O que e
Arquitetura onde aplicacao e dividida em servicos pequenos e independentes.

## Principios

### Single Responsibility
- Cada servico faz uma coisa bem
- Bounded context claro
- Time autonomo por servico

### Independencia
- Deploy independente
- Tecnologias diferentes
- Times diferentes

### Comunicacao
- APIs bem definidas
- Mensagens assincronas
- Event-driven quando possivel

## Padroes de Comunicacao

### Sincrono (HTTP/REST)
// Service A chama Service B
const response = await fetch('http://service-b/api/users/123');
const user = await response.json();

Pros:
- Simples de entender
- Resposta imediata

Cons:
- Acoplamento temporal
- Cascata de falhas
- Latencia

### Assincrono (Message Queue)
// Service A publica evento
await rabbitmq.publish('user.created', { userId: 123 });

// Service B consome evento
rabbitmq.subscribe('user.created', async (message) => {
  await processUser(message.userId);
});

Pros:
- Desacoplamento
- Escalabilidade
- Resiliencia

Cons:
- Complexidade
- Eventual consistency
- Debugging mais dificil

## Service Discovery

### Consul
// Registrar servico
consul.agent.service.register({
  name: 'user-service',
  address: '10.0.0.1',
  port: 8080
});

// Descobrir servico
const instances = await consul.health.service('user-service');
const instance = instances[0];
const url = `http://${instance.Service.Address}:${instance.Service.Port}`;

### Kubernetes
// Service automaticamente descoberto
const response = await fetch('http://user-service.default.svc.cluster.local/api/users');

## API Gateway

### Funcoes
- Roteamento de requests
- Autenticacao centralizada
- Rate limiting
- Load balancing
- Circuit breaker

### Exemplo (Kong)
// Kong config
services:
  - name: user-service
    url: http://user-service:8080
    routes:
      - paths: ['/api/users']

// Client chama gateway
const response = await fetch('https://api.example.com/api/users');
// Gateway roteia para user-service

## Circuit Breaker

### Implementacao
class CircuitBreaker {
  constructor(fn, options = {}) {
    this.fn = fn;
    this.state = 'CLOSED';
    this.failureCount = 0;
    this.successCount = 0;
    this.threshold = options.threshold || 5;
    this.timeout = options.timeout || 60000;
  }
  
  async call(...args) {
    if (this.state === 'OPEN') {
      if (Date.now() - this.lastFailure > this.timeout) {
        this.state = 'HALF_OPEN';
      } else {
        throw new Error('Circuit breaker is OPEN');
      }
    }
    
    try {
      const result = await this.fn(...args);
      this.onSuccess();
      return result;
    } catch (error) {
      this.onFailure();
      throw error;
    }
  }
  
  onSuccess() {
    this.failureCount = 0;
    if (this.state === 'HALF_OPEN') {
      this.state = 'CLOSED';
    }
  }
  
  onFailure() {
    this.failureCount++;
    this.lastFailure = Date.now();
    if (this.failureCount >= this.threshold) {
      this.state = 'OPEN';
    }
  }
}

// Uso
const breaker = new CircuitBreaker(callUserService);
const user = await breaker.call(userId);

## Data Management

### Database per Service
- Cada servico tem seu proprio banco
- Isolamento de dados
- Tecnologias diferentes

### Saga Pattern
// Transacao distribuida
async function createOrder(data) {
  try {
    const order = await orderService.create(data);
    await inventoryService.reserve(order.items);
    await paymentService.charge(order.total);
    return order;
  } catch (error) {
    // Compensating transactions
    await paymentService.refund(order.id);
    await inventoryService.release(order.items);
    await orderService.cancel(order.id);
    throw error;
  }
}

### Event Sourcing
// Armazenar eventos, nao estado
await eventStore.append('OrderCreated', { orderId: 123, userId: 456 });
await eventStore.append('ItemAdded', { orderId: 123, productId: 789 });

// Reconstruir estado
const events = await eventStore.getEvents('OrderCreated', 123);
const order = events.reduce((state, event) => applyEvent(state, event), {});

## Observabilidade

### Distributed Tracing
// OpenTelemetry
const tracer = trace.getTracer('user-service');

async function getUser(id) {
  return tracer.startActiveSpan('getUser', async (span) => {
    span.setAttribute('user.id', id);
    try {
      const user = await db.query('SELECT * FROM users WHERE id = ?', [id]);
      return user;
    } finally {
      span.end();
    }
  });
}

### Centralized Logging
// ELK Stack (Elasticsearch, Logstash, Kibana)
logger.info('User created', { userId: 123, email: 'user@example.com' });
// Logs enviados para Elasticsearch
// Visualizados no Kibana

### Metrics
// Prometheus
const requestCounter = new prometheus.Counter({
  name: 'http_requests_total',
  help: 'Total HTTP requests',
  labelNames: ['method', 'endpoint', 'status']
});

requestCounter.inc({ method: 'GET', endpoint: '/users', status: 200 });

## Deployment

### Kubernetes
apiVersion: apps/v1
kind: Deployment
metadata:
  name: user-service
spec:
  replicas: 3
  selector:
    matchLabels:
      app: user-service
  template:
    metadata:
      labels:
        app: user-service
    spec:
      containers:
      - name: user-service
        image: user-service:1.0.0
        ports:
        - containerPort: 8080

### Docker Compose
version: '3'
services:
  user-service:
    build: ./user-service
    ports:
      - '8080:8080'
    depends_on:
      - postgres
  
  order-service:
    build: ./order-service
    ports:
      - '8081:8081'
  
  postgres:
    image: postgres:14
    environment:
      POSTGRES_DB: mydb

## Desafios

### Complexidade
- Mais servicos para gerenciar
- Comunicacao entre servicos
- Debugging distribuido

### Data Consistency
- Eventual consistency
- Transacoes distribuidas
- Sincronizacao de dados

### Deployment
- Coordenacao de deploys
- Versionamento de APIs
- Rollback complexo

## Quando Usar
- Times grandes e autonomos
- Necessidade de escalar independentemente
- Tecnologias heterogeneas
- Deploy frequente

## Quando Nao Usar
- Times pequenos
- Aplicacao simples
- Nao ha necessidade de escala
- Overhead nao justifica