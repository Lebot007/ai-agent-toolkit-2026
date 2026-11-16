# Agent Patterns - Padroes de Agentes de IA

## O que e
Padroes arquiteturais para construir agentes de IA eficazes.

## Padroes Fundamentais

### ReAct (Reasoning + Acting)
- Alternar entre raciocinio e acao
- Thought -> Action -> Observation -> Thought
- Melhor para tarefas multi-step

Exemplo:
  Thought: Preciso encontrar informacoes sobre X
  Action: search(X)
  Observation: [resultados]
  Thought: Com base nos resultados, posso concluir Y
  Action: answer(Y)

### Plan-and-Solve
- Planejar antes de executar
- Decompor problema em etapas
- Executar plano passo a passo

### Reflexion
- Auto-reflexao apos execucao
- Aprender com erros
- Melhorar iterativamente

### Tool Use
- Agentes usam ferramentas externas
- APIs, bancos de dados, calculadoras
- Decidir quando e qual ferramenta usar

## Padroes Avancados

### Multi-Agent Systems
- Multiplos agentes especializados
- Colaboracao ou competencia
- Orquestracao de trabalho

Orchestrator Agent:
  - Research Agent (busca informacoes)
  - Analysis Agent (analisa dados)
  - Writer Agent (redige resposta)
  - Reviewer Agent (valida qualidade)

### Hierarchical Agents
- Manager agent delega para workers
- Workers reportam resultados
- Escalacao quando necessario

### Memory-Augmented Agents
- Memoria de curto prazo (contexto)
- Memoria de longo prazo (vector DB)
- Recuperacao contextual

## Ferramentas e Frameworks

### LangChain Agents
from langchain.agents import initialize_agent, Tool
from langchain.llms import OpenAI

tools = [
    Tool(name='Search', func=search_func, description='Use for searching'),
    Tool(name='Calculator', func=calc_func, description='Use for math')
]

agent = initialize_agent(tools, llm, agent='zero-shot-react-description')
result = agent.run('What is 2+2 and who is the president?')

### AutoGPT
- Agentes autonomos
- Definir objetivo, executar sem intervencao
- Auto-prompting e planejamento

### CrewAI
- Multi-agent framework
- Roles e goals definidos
- Colaboracao estruturada

### LangGraph
- Agentes como grafos
- Ciclos, branches, estado
- Ideal para workflows complexos

## Best Practices

### Prompt Engineering para Agentes
- Definir papel claramente
- Fornecer exemplos de uso de ferramentas
- Especificar formato de saida
- Incluir estrategias de fallback

### Error Handling
- Retry com backoff exponencial
- Fallback para abordagem mais simples
- Logging detalhado de acoes
- Validacao de resultados

### Limites e Guardrails
- Maximo de iteracoes
- Timeout por tarefa
- Validacao de outputs
- Sandbox de execucao

## Trade-offs
- Autonomia vs controle
- Velocidade vs precisao
- Custo vs qualidade

## Quando Usar
- Tarefas multi-step complexas
- Necessidade de ferramentas externas
- Processos que requerem julgamento
- Automacao de workflows