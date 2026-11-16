# Video e Audio Tools

Ferramentas para criacao, processamento e manipulacao de video e audio programaticamente.

## Remotion

**Repo:** github.com/remotion-dev/remotion

### O que e
Framework React para criar videos programaticamente usando componentes React.

### Features
- Videos como componentes React
- Renderizacao server-side ou client-side
- Animacoes com React Spring, Framer Motion
- Audio mixing e synchronization
- Data-driven video generation

### Uso
- Video marketing automatizado
- Personalizacao em escala
- Data visualization em video
- Social media content generation

### Exemplo Basico
import {Composition} from 'remotion';

export const RemotionVideo = () => {
  return (
    <>
      <Composition
        id="MyVideo"
        component={MyComposition}
        durationInFrames={150}
        fps={30}
        width={1920}
        height={1080}
      />
    </>
  );
};

## HyperFrames

**Repo:** github.com/heygen-com/hyperframes

### O que e
Framework para criacao de videos com IA, focado em avatares e content generation.

### Features
- AI avatar generation
- Text-to-video
- Voice synthesis
- Multi-language support
- API-first approach

### Casos de Uso
- Training videos
- Product demos
- Marketing content
- Personalized messages

## FFmpeg

**Repo:** github.com/FFmpeg/FFmpeg

### O que e
Ferramenta completa para processamento de audio e video via linha de comando.

### Capabilities
- Conversao de formatos (MP4, AVI, MOV, WebM, etc)
- Compressao e otimizacao
- Extracao de audio de video
- Corte e concatenacao
- Adicao de watermarks
- Streaming (RTMP, HLS)
- Aplicacao de filtros

### Comandos Essenciais
# Converter formato
ffmpeg -i input.avi output.mp4

# Extrair audio
ffmpeg -i video.mp4 -vn -acodec mp3 audio.mp3

# Cortar video (0s a 30s)
ffmpeg -i input.mp4 -ss 0 -t 30 -c copy output.mp4

# Reduzir tamanho
ffmpeg -i input.mp4 -vf scale=1280:720 -crf 28 output.mp4

# Adicionar watermark
ffmpeg -i input.mp4 -i watermark.png -filter_complex overlay output.mp4

## Whisper

**Repo:** github.com/ggml-org/whisper.cpp

### O que e
Modelo de speech-to-text da OpenAI, otimizado em C++ para performance.

### Features
- Transcricao multi-lingua (99 idiomas)
- Traducao para ingles
- Time-stamping
- Speaker diarization
- Roda localmente (offline)

### Modelos
- **tiny:** 39M params, rapido, menos preciso
- **base:** 74M params, bom balanco
- **small:** 244M params, boa precisao
- **medium:** 769M params, alta precisao
- **large:** 1550M params, melhor precisao

### Uso
# Python
import whisper
model = whisper.load_model('base')
result = model.transcribe('audio.mp3')
print(result['text'])

# whisper.cpp (C++)
./main -m models/ggml-base.bin -f audio.wav

## yt-dlp

**Repo:** github.com/yt-dlp/yt-dlp

### O que e
Ferramenta para download de videos de YouTube e 1000+ sites.

### Features
- Download de videos e audio
- Extracao de metadados
- Suporte a playlists
- Legendas automaticas
- Selecao de qualidade
- Proxy support

### Comandos Essenciais
# Download video
yt-dlp 'https://youtube.com/watch?v=VIDEO_ID'

# Download audio apenas
yt-dlp -x --audio-format mp3 URL

# Melhor qualidade
yt-dlp -f 'bestvideo[ext=mp4]+bestaudio[ext=m4a]' URL

# Download playlist
yt-dlp --yes-playlist PLAYLIST_URL

# Com legendas
yt-dlp --write-auto-sub --sub-lang pt URL

# Extrair metadados
yt-dlp --dump-json URL > metadata.json

## Integracao

### Pipeline Exemplo
1. yt-dlp: download video do YouTube
2. FFmpeg: extrair audio
3. Whisper: transcrever audio
4. Remotion: gerar video com transcricao
5. FFmpeg: otimizar para web

### Casos de Uso
- Content repurposing
- Video summarization
- Subtitle generation
- Video translation
- Accessibility features