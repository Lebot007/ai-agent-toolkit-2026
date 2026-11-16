# Plugin Creator

Skill especializado em criar, desenvolver e aprimorar plugins e integracoes para IAs e agentes.

## O que faz
- Projeta arquitetura de plugins desde o zero
- Define interfaces claras e extensiveis
- Implementa hooks e lifecycle methods
- Documenta APIs e exemplos de uso
- Testa compatibilidade e versionamento

## Arquitetura de Plugins

### Estrutura Padrao
my-plugin/
  package.json (ou pyproject.toml)
  README.md
  src/
    index.ts (entry point)
    hooks/ (before, after, error)
    commands/
    utils/
  tests/ (unit, integration)
  docs/

### Lifecycle Hooks
- init: plugin e carregado
- beforeTask: antes de cada tarefa
- afterTask: depois de cada tarefa
- onError: tratamento de erros
- shutdown: cleanup ao finalizar

## Padroes de Design

### Command Pattern
interface Command {
  name: string;
  description: string;
  execute(context): Promise<Result>;
}

### Observer Pattern
class PluginEventBus {
  on(event, handler): void;
  emit(event, data): void;
}

## Tecnologias Comuns

### JavaScript/TypeScript
- ESM modules
- Plugin registries
- Dynamic imports
- Type-safe APIs

### Python
- Entry points (setuptools)
- Decorators
- Abstract base classes
- Pydantic para schemas

## Exemplos de Plugins

### MCP Server Plugin
- Conecta servicos externos (Slack, GitHub, DB)
- Define tools que agentes podem chamar
- Gerencia autenticacao e rate limiting

### Claude Code Plugin
- Skills customizados
- Slash commands
- Sub-agentes especializados
- Integracoes com ferramentas

### Browser Extension
- Content scripts
- Background workers
- Popup UI
- Storage API

## Testing

### Unit Tests
- Funcoes isoladas
- Mocks de dependencias
- Cobertura > 80%

### Integration Tests
- Plugin completo carregado
- Interacao com host
- Casos de uso reais

## Publicacao

### NPM
npm version patch
npm publish

### PyPI
python -m build
twine upload dist/*

### GitHub Marketplace
- Submeter para review
- Badge oficial
- Discoverability