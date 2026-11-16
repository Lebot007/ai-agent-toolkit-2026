# Edge AI & On-Device Processing - IA na Borda e Processamento Local

## O que e
Execução de modelos de IA diretamente no dispositivo do usuário (celular, navegador, IoT) em vez de na nuvem.

## Vantagens
- Latência zero de rede
- Privacidade total (dados nunca saem do dispositivo)
- Funcionamento offline
- Custo zero de inferência na nuvem

## Tecnologias
- WebLLM: Executa modelos Llama, Phi diretamente no navegador via WebGPU
- Core ML (Apple) / ML Kit (Android): Frameworks nativos para mobile
- Ollama / LM Studio: Execução local em desktops

## Desafios
- Limitações de memória e potência de processamento do dispositivo
- Necessidade de modelos altamente otimizados e quantizados (ex: Phi-3, Gemma 2B)
