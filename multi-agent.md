# Multi-Agent Systems - Sistemas Multi-Agente

## O que e
Multiplos agentes de IA trabalhando juntos para resolver problemas complexos.

## Arquiteturas

### Centralizada
- Um agente orquestrador
- Delega tarefas para especialistas
- Agrega resultados

### Descentralizada
- Agentes se comunicam diretamente
- Sem coordenador central
- Mais resiliente

### Hierarquica
- Manager agents supervisam workers
- Workers reportam resultados
- Escalacao quando necessario

## Padroes de Colaboracao

### Pipeline
Agent 1 -> Agent 2 -> Agent 3 -> Result
- Cada agente faz uma transformacao
- Output de um e input do proximo

### Parallel
Agent 1 -> Result
Agent 2 -> Result
Agent 3 -> Result
- Agentes trabalham em paralelo
- Resultados agregados no final

### Debate
Agent 1 vs Agent 2 -> Judge -> Winner
- Agentes argumentam posicoes diferentes
- Judge decide melhor resposta
- Melhora qualidade

## Frameworks

### CrewAI
from crewai import Crew, Agent, Task

researcher = Agent(
    role='Researcher',
    goal='Find accurate information',
    backstory='Expert researcher with years of experience'
)

writer = Agent(
    role='Writer',
    goal='Write clear and engaging content',
    backstory='Professional writer'
)

research_task = Task(
    description='Research topic X',
    agent=researcher
)

write_task = Task(
    description='Write article based on research',
    agent=writer
)

crew = Crew(agents=[researcher, writer], tasks=[research_task, write_task])
result = crew.kickoff()

### AutoGen
from autogen import AssistantAgent, UserProxyAgent

assistant = AssistantAgent('assistant', llm_config=llm_config)
user_proxy = UserProxyAgent('user_proxy', human_input_mode='NEVER')

user_proxy.initiate_chat(
    assistant,
    message='Write a Python function to calculate fibonacci numbers'
)

### LangGraph
from langgraph.graph import StateGraph, END
from typing import TypedDict, Annotated

class AgentState(TypedDict):
    messages: Annotated[list, add_messages]

def researcher(state):
    # Research logic
    return {'messages': [research_result]}

def writer(state):
    # Writing logic
    return {'messages': [written_content]}

workflow = StateGraph(AgentState)
workflow.add_node('researcher', researcher)
workflow.add_node('writer', writer)
workflow.add_edge('researcher', 'writer')
workflow.add_edge('writer', END)

app = workflow.compile()
result = app.invoke({'messages': []})

## Padroes de Comunicacao

### Message Passing
- Agentes trocam mensagens
- Formato estruturado (JSON)
- Queue ou pub/sub

### Shared State
- Estado compartilhado entre agentes
- Cada agente le e modifica
- Sincronizacao necessaria

### Blackboard
- Espaco compartilhado de trabalho
- Agentes leem e escrevem
- Conhecimento acumulado

## Desafios

### Coordenacao
- Evitar trabalho duplicado
- Sincronizar agentes
- Resolver conflitos

### Comunicacao
- Formato de mensagens
- Latencia de comunicacao
- Perda de mensagens

### Consistencia
- Manter estado consistente
- Evitar race conditions
- Transacoes distribuidas

## Best Practices

### Design
- Definir responsabilidades claras
- Minimizar acoplamento
- Maximizar coesao

### Monitoring
- Log de todas as interacoes
- Track de performance
- Alertas para falhas

### Testing
- Testar agentes individualmente
- Testar integracao
- Simular cenarios de falha

## Quando Usar
- Problemas complexos multi-dominio
- Necessidade de especializacao
- Processos que beneficiam de paralelismo
- Sistemas que precisam de redundancia