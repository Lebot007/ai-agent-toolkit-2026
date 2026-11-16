# Optimized Tokenizers - Tokenizadores Otimizados

## O que e
Uso de tokenizadores mais eficientes para reduzir o tempo de pré-processamento e o número de tokens gerados.

## Técnicas
- Tiktoken (OpenAI): Tokenizador muito rápido em Rust, padrão para modelos GPT
- BPE (Byte-Pair Encoding) otimizado: Vocabulários maiores podem representar palavras comuns com menos tokens
- Character-level ou Word-level para tarefas específicas onde BPE não é necessário

## Impacto na Velocidade
- Tokenização rápida é crítica para o Time to First Token (TTFT) em prompts longos
- Menos tokens = menos computação no modelo = geração mais rápida e barata
- Compressão de prompt: usar instruções concisas para reduzir a contagem de tokens antes mesmo da tokenização

## Ferramentas
- `tiktoken` library para contagem e decodificação rápida
- Tokenizadores personalizados treinados no domínio específico para melhor compressão
