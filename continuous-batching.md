# Continuous Batching - Batching Contínuo (In-Flight Batching)

## O que e
Técnica de agendamento que permite que novas requisições entrem no batch de inferência assim que houver espaço, sem esperar o batch atual terminar.

## Comparação
- Static Batching: Espera todos os requests do batch terminarem antes de iniciar o próximo (alta latência para requests curtos)
- Continuous Batching: Iteração por iteração, verifica se algum request terminou e insere um novo no lugar (throughput máximo, latência baixa)

## Implementação
- vLLM (PagedAttention) é o padrão ouro para continuous batching
- Requer gerenciamento de memória de KV cache eficiente para evitar fragmentação
- Essencial para servir múltiplos usuários simultaneamente em uma única GPU

## Benefícios
- Aumento de 10x a 20x no throughput comparado ao static batching
- Latência consistente independentemente do tamanho da geração
