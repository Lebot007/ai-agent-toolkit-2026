# Tree-of-Thought e Estruturas Avancadas

## Tree of Thought (ToT)
- Repo: github.com/princeton-nlp/tree-of-thought-llm
- Explorar multiplos caminhos em paralelo
- Avaliar cada no (thought) com score
- Backtracking quando necessario
- Busca BFS ou DFS

### Implementacao
1. Gerar k pensamentos iniciais
2. Para cada pensamento: avaliar viabilidade (1-10)
3. Manter top-m pensamentos
4. Expandir cada um
5. Repetir ate solucao

### Casos de Uso
- Sudoku, 24 Game
- Planejamento complexo
- Criacao de historias

## Graph of Thought (GoT)
- Pensamentos como nos em grafo
- Arestas = relacoes logicas
- Permite merge de pensamentos

## Algorithm of Thought (AoT)
- Internalizar algoritmo no LLM
- Um unico forward pass
- Reduz overhead

## Skeleton-of-Thought
1. Gerar esqueleto da resposta
2. Expandir cada ponto em paralelo
3. Combinar resultados
- 2-3x mais rapido

## Ferramentas

### LangGraph
- Repo: github.com/langchain-ai/langgraph
- Agentes como grafos
- Ciclos, branches, estado