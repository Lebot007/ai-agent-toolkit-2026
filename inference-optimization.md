# Otimizacao de Inferencia

## Engines de Alta Performance

### vLLM
- Repo: github.com/vllm-project/vllm
- PagedAttention para KV cache
- Continuous batching
- 14-24x throughput vs HuggingFace

### TensorRT-LLM
- Repo: github.com/NVIDIA/TensorRT-LLM
- NVIDIA GPUs otimizados
- Quantizacao INT8/FP8
- In-flight batching

### SGLang
- Repo: github.com/sgl-project/sglang
- RadixAttention (prefix caching)
- 5x mais rapido que vLLM para structured gen

### llama.cpp
- Repo: github.com/ggerganov/llama.cpp
- CPU e GPU
- GGUF format
- Quantizacao: Q4_0, Q5_K_M, Q8_0

### Ollama
- Site: ollama.ai
- Facilita uso local
- Wrapper para llama.cpp

## Quantizacao

### Metodos
- GPTQ: post-training, INT4
- AWQ: activation-aware, preserva qualidade
- GGUF: llama.cpp, varios niveis
- bitsandbytes: 4-bit, 8-bit

### Trade-offs
- Q4: 4x menor, ~1% perda
- Q5: balanco bom
- Q8: quase sem perda

## KV Cache

### PagedAttention (vLLM)
- Divide KV cache em paginas
- Evita fragmentacao
- 96% reducao em waste

### Prefix Caching
- Compartilha prefixos comuns
- Ideal para system prompts

## Speculative Decoding
- Pequeno modelo rascunha tokens
- Modelo grande verifica
- 2-3x speedup sem perda de qualidade

## Batching Strategies

### Static Batching
- Espera batch completo
- Ineficiente para latencia

### Continuous Batching
- Adiciona requests em voo
- Muito melhor throughput

### Chunked Prefill
- Processa prefill em chunks
- Mistura com decode

## Ferramentas
- lmdeploy: github.com/InternLM/lmdeploy
- ExLlamaV2: github.com/turboderp/exllamav2
- MLX: github.com/ml-explore/mlx (Apple Silicon)