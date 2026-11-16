# Quantization for Speed - Quantização para Velocidade

## O que e
Redução da precisão numérica dos pesos do modelo (ex: de FP16 para INT8 ou INT4) para acelerar a inferência e reduzir o uso de memória.

## Técnicas
- PTQ (Post-Training Quantization): Quantiza o modelo após o treinamento (ex: AWQ, GPTQ, GGUF)
- QAT (Quantization-Aware Training): Treina o modelo já considerando a quantização (melhor qualidade, mas mais caro)

## Formatos Populares
- GGUF (llama.cpp): Excelente para execução em CPU e Apple Silicon
- AWQ (AutoAWQ): Preserva melhor a qualidade em 4-bit, ideal para GPUs NVIDIA
- FP8: Suportado em GPUs H100, oferece bom balanço entre velocidade e precisão

## Trade-offs
- INT4: 4x menos memória, ~2x mais rápido, pequena perda de qualidade
- INT8: 2x menos memória, ~1.5x mais rápido, perda de qualidade quase imperceptível
