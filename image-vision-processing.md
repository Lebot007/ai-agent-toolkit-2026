# Image & Vision Processing

## Pre-processing
- Compressao: Reduzir resolucao e qualidade para economizar tokens
- Formato: Converter para WEBP ou JPEG otimizado
- Crop: Remover bordas desnecessarias

## Vision Models
- GPT-4V, Claude 3: Analise de conteudo, extracao de texto, descricao
- LayoutLM: Extracao de informacoes de formularios e recibos

## Implementacao
- Converter imagem para base64 no frontend
- Enviar como multipart/form-data ou base64 no payload
- Cache de resultados de vision para imagens identicas

## UX/UI
- Preview da imagem com opcao de remover
- Indicador de tamanho do arquivo