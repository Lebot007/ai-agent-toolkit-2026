# Speculative Decoding - Decodificação Especulativa para LLMs

## O que e
Técnica que usa um modelo pequeno e rápido para rascunhar tokens, que são então verificados em paralelo por um modelo grande e lento.

## Como Funciona
1. Modelo pequeno (Draft) gera N tokens rapidamente
2. Modelo grande (Target) avalia todos os N tokens de uma vez
3. Tokens corretos são aceitos, incorretos são descartados e o modelo grande gera o próximo
4. Resultado: Mesma qualidade do modelo grande, mas com velocidade próxima do modelo pequeno

## Implementação
- Suportado nativamente no vLLM e TensorRT-LLM
- Requer dois modelos compatíveis (ex: Llama-3-8B como draft, Llama-3-70B como target)
- Aceleração de 2x a 3x em tarefas de geração de texto

## Casos de Uso
- Chatbots que exigem baixa latência
- Geração de código em tempo real
- Qualquer aplicação onde a velocidade de tokens por segundo é crítica
