# Chain-of-Thought Avancado

## Variacoes de CoT

### Zero-shot CoT
- Prompt: Vamos pensar passo a passo
- Aumenta raciocinio em 40%+
- Ideal para problemas matematicos

### Few-shot CoT
- 2-3 exemplos com raciocinio completo
- Estrutura: pergunta > passos > resposta
- Melhor para tarefas especificas

### Self-Consistency
- Gerar N caminhos de raciocinio diferentes
- Votar pela resposta mais frequente
- Aumenta precisao em 10-15%
- Usa temperature alta (0.7-1.0)

## Tecnicas Avancadas

### Least-to-Most Prompting
1. Decompor problema em subproblemas
2. Resolver subproblemas em ordem
3. Combinar solucoes

### Decomposition Prompting
- Quebrar problemas complexos
- Resolver cada parte independentemente
- Sintetizar resposta final

### Maieutic Prompting
- Gerar explicacao do problema
- Identificar contradicoes
- Refinar entendimento iterativamente

## Verificacao

### Self-Verification
1. Gerar resposta
2. Verificar: faz sentido?
3. Contra-provar: se X entao Y?

### Reverse Engineering
- Comecar da resposta
- Reconstruir passos
- Validar logica

## Frameworks

### DSPy
- Repo: github.com/stanfordnlp/dspy
- Programmatic prompting
- Auto-optimizacao de prompts

### Guidance
- Repo: github.com/guidance-ai/guidance
- Structured generation
- Controle de output