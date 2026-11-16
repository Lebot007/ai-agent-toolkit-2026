# Prompt Engineering Avancado

## Tecnicas Estruturadas

### Role-Playing
- Voce e um especialista em X
- Define persona clara
- Contextualiza conhecimento

### Structured Output
- JSON mode
- Function calling
- Schemas rigorosos

### Multi-step Prompting
- Planejar antes de executar
- Validar antes de concluir
- Refletir sobre resultado

## Meta-Prompting

### Prompt Generator
- LLM gera prompts para tarefas
- Otimiza automaticamente

### Self-Refine
1. Gerar resposta inicial
2. Criticar a resposta
3. Refinar com feedback

### Reflexion
- Aprender com erros
- Manter memoria de falhas
- Evitar repetir

## Few-Shot Avancado

### Example Selection
- k-NN para encontrar exemplos similares
- Diversidade nos exemplos
- Balanceamento de dificuldades

### Active Prompting
- Selecionar exemplos informativos
- Maximizar ganho de informacao

## Frameworks

### DSPy
- Repo: github.com/stanfordnlp/dspy
- Assinaturas, modulos, otimizacao
- Compila prompts automaticamente

### Instructor
- Repo: github.com/jxnl/instructor
- Pydantic + LLMs
- Validacao automatica

### Guardrails
- Repo: github.com/ShreyaR/guardrails
- Validacao de output
- Re-ask quando falha