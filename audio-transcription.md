# Audio Transcription

## STT Engines
- Whisper (OpenAI): Alta precisao, multi-idioma
- Whisper.cpp: Execucao local, privacidade
- AssemblyAI / Deepgram: APIs especializadas com diarization

## Pre-processing
- Normalizacao de volume
- Remocao de ruido de fundo
- Conversao para formato suportado (WAV, MP3, 16kHz)

## Implementacao
- Upload assincrono com polling ou WebSocket para status
- Exibir transcricao parcial enquanto processa
- Permitir edicao manual da transcricao antes de enviar para IA

## UX/UI
- Player de audio integrado
- Waveform visual
- Botao de gravar direto no browser