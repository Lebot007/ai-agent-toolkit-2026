# API Design - Design de APIs REST

## Principios REST

### Recursos (Nouns)
- URLs representam recursos
- Usar substantivos no plural
- Hierarquia logica

Bom:
GET /api/users
GET /api/users/123
GET /api/users/123/orders

Ruim:
GET /api/getUser
GET /api/user/123/getOrders

### HTTP Methods (Verbs)
- GET: Buscar recurso(s)
- POST: Criar recurso
- PUT: Atualizar recurso completo
- PATCH: Atualizacao parcial
- DELETE: Remover recurso

### Status Codes

Sucesso:
- 200 OK: Request bem-sucedido
- 201 Created: Recurso criado
- 204 No Content: Sucesso sem body

Cliente:
- 400 Bad Request: Request invalido
- 401 Unauthorized: Nao autenticado
- 403 Forbidden: Sem permissao
- 404 Not Found: Recurso nao existe
- 409 Conflict: Conflito
- 422 Unprocessable Entity: Validacao falhou

Servidor:
- 500 Internal Server Error
- 503 Service Unavailable

## Endpoints CRUD

GET    /api/users          # Listar usuarios
GET    /api/users/123      # Buscar usuario especifico
POST   /api/users          # Criar usuario
PUT    /api/users/123      # Atualizar usuario completo
PATCH  /api/users/123      # Atualizacao parcial
DELETE /api/users/123      # Remover usuario

## Filtering, Sorting, Pagination

### Filtering
GET /api/users?status=active
GET /api/users?role=admin&department=engineering
GET /api/products?price_min=100&price_max=500

### Sorting
GET /api/users?sort=name
GET /api/users?sort=-created_at  # Descending
GET /api/users?sort=name,-created_at  # Multiple

### Pagination

#### Offset-based
GET /api/users?page=2&limit=20

#### Cursor-based (melhor para grandes datasets)
GET /api/users?cursor=eyJpZCI6MTAwfQ&limit=20

## Versionamento

### URL Path
GET /api/v1/users
GET /api/v2/users

### Header
GET /api/users
Accept: application/vnd.myapi.v1+json

## Best Practices

### Design
- Usar substantivos no plural
- URLs minusculas
- Hierarquia logica
- Consistencia

### Performance
- Pagination sempre
- Campos opcionais (fields parameter)
- Compressao (gzip)
- Caching apropriado

### Seguranca
- Validar todos os inputs
- Autenticacao em todos os endpoints
- Rate limiting
- Logs de auditoria

## Ferramentas

### Frameworks
- Express (Node.js)
- FastAPI (Python)
- Spring Boot (Java)
- Gin (Go)

### Documentacao
- OpenAPI (Swagger)
- Postman
- Redoc

## Quando Usar
- Aplicacoes web/mobile
- Integracao entre sistemas
- Microservicos
- APIs publicas
