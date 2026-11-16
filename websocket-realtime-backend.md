# WebSocket & Real-time Backend

## Implementacao
- Socket.io (Node.js) ou FastAPI WebSockets (Python)
- Gerenciamento de conexoes ativas por usuario/sessao

## Padroes de Mensagem
- JSON estruturado: { type: 'message', content: '...', metadata: {} }
- Heartbeat/Ping-Pong para manter conexao viva

## Escalabilidade
- Redis Pub/Sub para broadcast entre multiplos servidores
- Sticky sessions no load balancer se necessario

## Fallback
- Fallback para SSE ou HTTP polling se WebSocket for bloqueado