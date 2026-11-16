# Multi-Agent Debate & Consensus - Debate e Consenso Multi-Agente

## O que e
Técnica onde múltiplos agentes com personas ou perspectivas diferentes discutem um problema para chegar a uma solução mais robusta.

## Padrões
- Debate: Agente A propõe, Agente B critica, Agente A refina
- Jury: Múltiplos agentes avaliam independentemente, um "juiz" agrega os votos
- Consensus: Agentes negociam até que todos concordem com uma solução

## Implementação
- LangGraph para orquestrar o fluxo de debate
- Prompts específicos para cada persona (ex: "Advogado do Diabo", "Otimista", "Cético")
- Critérios de parada: Número máximo de rodadas ou convergência de respostas

## Benefícios
- Redução de alucinações
- Descoberta de edge cases
- Soluções mais balanceadas e menos enviesadas
