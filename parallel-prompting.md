# Parallel Prompting - Prompting em Paralelo

## O que e
Técnica de dividir uma tarefa complexa em múltiplas subtarefas independentes e processá-las simultaneamente em diferentes chamadas de API.

## Padrões
- Map-Reduce: Dividir documento em chunks, processar cada chunk em paralelo, agregar resultados
- Ensemble: Enviar o mesmo prompt para 3 modelos diferentes (ou 3 vezes para o mesmo) e agregar as respostas (votação ou síntese)
- Branching: Explorar múltiplos caminhos de raciocínio ao mesmo tempo (Tree of Thoughts paralelo)

## Implementação
- `asyncio.gather` em Python ou `Promise.all` em JavaScript
- Requer que as subtarefas sejam verdadeiramente independentes
- Aumenta o custo de tokens, mas reduz drasticamente a latência total percebida

## Casos de Uso
- Análise de múltiplos documentos longos
- Geração de múltiplas variações de copy para A/B testing
- Validação cruzada rápida de fatos
