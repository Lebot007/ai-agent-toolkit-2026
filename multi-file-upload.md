# Multi-file Upload - Upload de Multiplos Tipos de Arquivo

## O que e
Sistema robusto para upload e processamento de diversos formatos de arquivo em chats de IA.

## Tipos de Arquivos Suportados
- Documentos: PDF, DOCX, TXT, CSV (extracao de texto, OCR, analise)
- Imagens: JPG, PNG, WEBP, SVG (Vision models)
- Audio: MP3, WAV, OGG (transcricao via Whisper)
- Video: MP4, WebM (extracao de frames, transcricao)

## Implementacao Frontend
- React Dropzone: Suporte a drag-and-drop, validacao de tipo e tamanho
- Preview de arquivos: Thumbnails para imagens, icones para docs

## Processamento Backend
- Chunking para arquivos grandes (5MB chunks)
- Validacao de seguranca: verificar MIME type real, scan de virus
- Sanitizacao de nomes de arquivo

## Integracao com IA
- Vision Models: enviar imagem em base64 ou URL
- Document Parsing: PyPDF2, pdfplumber, unstructured, python-docx, pandas

## UX/UI Best Practices
- Barra de progresso para uploads grandes
- Indicador claro de tipos aceitos
- Mensagens de erro amigaveis
- Compressao automatica de imagens no cliente
