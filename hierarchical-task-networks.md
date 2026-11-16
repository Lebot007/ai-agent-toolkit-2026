# Hierarchical Task Networks (HTN) - Redes Hierárquicas de Tarefas

## O que e
Método de planejamento onde tarefas complexas são decompostas recursivamente em subtarefas primitivas.

## Arquitetura
- Tarefas de alto nível (ex: "Planejar viagem")
- Métodos de decomposição (ex: "Para planejar viagem, reserve voo E reserve hotel")
- Tarefas primitivas (ex: "Chamar API de reserva de voo")

## Implementação
- PyHOP ou SHOP2 para planejamento HTN
- Integração com LLM para gerar métodos de decomposição dinamicamente
- Backtracking quando uma subtarefa falha

## Casos de Uso
- Logística e cadeia de suprimentos
- Planejamento de projetos complexos
- Jogos de estratégia com IA
