# 🦸 Superpowers - Metodologia de Desenvolvimento

Framework completo de engenharia de software que transforma agentes de IA em desenvolvedores sênior.
**Repo:** davidjosephhayward/superpowers

## 🎯 Pilares

### 1. Planejamento Estratégico
- Decomposição de tarefas em subtarefas gerenciáveis
- Estimativa de esforço e complexidade
- Definição de critérios de aceitação
- Identificação de riscos e dependências

### 2. TDD (Test-Driven Development)
- Red-Green-Refactor: teste falhando > implementar > refatorar
- Cobertura: unitários, integração, E2E
- Testes como especificação viva
- Mocks e stubs para isolar dependências

### 3. Debugging Sistemático
- Reprodução do bug com caso de teste
- Isolamento: reduzir ao mínimo reproduzível
- Formulação de hipóteses
- Root cause analysis (não só sintomas)
- Post-mortem e documentação

### 4. Code Review
- Legibilidade e clareza
- Performance e otimizações
- Segurança (OWASP Top 10)
- Manutenibilidade (SOLID, DRY, KISS)

### 5. Colaboração Multi-Agent
- Orquestração de múltiplos agentes
- Especialização por papel
- Protocolos de comunicação claros
- Handoffs com contexto completo
- Validação cruzada entre agentes

## 📋 Workflow Completo

PLANNING > ARCHITECTURE > IMPLEMENTATION (TDD) > TESTING > REVIEW > DEPLOYMENT

## 🛠️ Skills Incluídos

- Planning: task decomposition, estimation, risk assessment
- Testing: Jest, Pytest, JUnit, Playwright, Cypress
- Debugging: profiling, memory leaks, concurrency
- Review: static analysis, security scanning, accessibility
- Collaboration: Git workflows, PR best practices

## 💡 Uso com Agentes

Exemplo: Implementar autenticação JWT
1. Planning: requisitos (login, logout, refresh), tarefas
2. Architecture: JWT RS256, Redis blacklist, refresh tokens rotativos
3. Implementation TDD: teste > código > refatorar
4. Testing: unit, integration, E2E
5. Review: segurança, performance, clareza
6. Deploy: CI/CD, staging, monitoring

## 🔗 Relacionados
- GStack: produtividade complementar
- TDD Expert: foco em testes
- Code Review: revisão especializada
