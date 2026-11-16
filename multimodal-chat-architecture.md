# Multi-Modal Chat Architecture

## O que e
Suporte nativo a texto, imagem, audio e video na mesma conversa.

## Implementacao
- Schema de mensagem unificado que suporta multiplos tipos de content
- Roteamento inteligente: enviar imagem para vision model, audio para Whisper
- Fusao de contextos: combinar transcricao de audio + analise de imagem no mesmo prompt

## UX/UI
- Indicadores visuais claros do tipo de midia
- Players e visualizadores embutidos
- Fallback gracioso se modelo nao suportar multimodal