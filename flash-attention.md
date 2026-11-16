# FlashAttention - Otimização de Atenção

## O que e
Algoritmo que calcula a atenção exata do transformer de forma mais rápida e com menos uso de memória, evitando materializar a matriz de atenção completa na HBM (High Bandwidth Memory).

## Como Funciona
- Tiling: Divide o cálculo em blocos que cabem na SRAM (memória rápida da GPU)
- Recomputação: Recalcula alguns valores intermediários em vez de salvá-los na HBM lenta

## Implementação
- FlashAttention-2: Otimizado para GPUs modernas (A100, H100), até 2x mais rápido que a v1
- Suportado nativamente em transformers, vLLM, e a maioria dos frameworks modernos
- Habilitar via `attn_implementation="flash_attention_2"` no Hugging Face

## Benefícios
- Treinamento e inferência mais rápidos
- Permite context windows muito maiores (ex: 128k, 1M tokens) sem OOM (Out of Memory)
