# Raciocinio Causal

## Judea Pearl e Causal Inference

### Ladder of Causation
1. Association: ver (correlacao)
2. Intervention: fazer (causalidade)
3. Counterfactuals: imaginar (o que seria se)

## Conceitos Fundamentais

### DAGs (Directed Acyclic Graphs)
- Nos = variaveis
- Arestas = relacoes causais
- Estruturas: chain, fork, collider

### Confounding
- Variavel que afeta tratamento e outcome
- Causa correlacao espuria
- Resolvido via adjustment

### do-calculus
- P(Y | do(X)) vs P(Y | X)
- Backdoor criterion
- Frontdoor criterion

## Ferramentas

### Python
- DoWhy: github.com/py-why/dowhy
- CausalNex: github.com/quantumblacklabs/causalnex
- EconML: github.com/py-why/econml

### R
- causalimpact
- dagitty
- ggdag

## Aplicacoes

### A/B Testing
- Estimar efeito causal de tratamento
- Controlar confounders

### Policy Evaluation
- Qual impacto de politica?
- Counterfactual analysis

### Medicine
- Efeito de droga em outcome
- Survival analysis

## LLMs e Causalidade

### Desafios
- LLMs aprendem correlacoes, nao causalidade
- Struggle com counterfactuals
- Confundem causa e efeito

### Melhorias
- Explicitar estrutura causal no prompt
- Usar DAGs como contexto
- Chain-of-thought causal