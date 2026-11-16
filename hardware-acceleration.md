# Hardware Acceleration - Aceleração de Hardware para IA

## O que e
Uso de hardware especializado para maximizar a velocidade de inferência e treinamento de modelos de IA.

## Tipos de Hardware
- GPU (NVIDIA H100, A100): Padrão da indústria, excelente para paralelismo massivo e FP8/FP16
- TPU (Google): Otimizado especificamente para operações de tensor, muito eficiente para treinamento e inferência em escala
- NPU/LPU (Groq, Apple Neural Engine): Arquiteturas especializadas para inferência de LLM com latência determinística e ultra-rápida

## Otimizações de Software para Hardware
- CUDA kernels customizados (ex: FlashAttention, PagedAttention)
- TensorRT-LLM: Compilação do modelo especificamente para a arquitetura da GPU NVIDIA
- vLLM: Otimizado para alto throughput em GPUs

## Escolha
- Latência crítica: Groq LPU ou NVIDIA com TensorRT
- Throughput crítico: NVIDIA A100/H100 com vLLM
- Custo-benefício: GPUs de geração anterior (A10, 4090) com quantização
