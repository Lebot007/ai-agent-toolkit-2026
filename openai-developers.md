# OpenAI Developers

Skill completo para desenvolver aplicacoes e agentes usando APIs e ferramentas OpenAI.

## APIs OpenAI

### Chat Completions
- GPT-4, GPT-4 Turbo, GPT-3.5 Turbo
- System, user, assistant messages
- Function calling
- Streaming responses
- JSON mode

### Assistants API
- Threads persistentes
- File search (RAG built-in)
- Code interpreter
- Function tools
- Streaming events

### Embeddings
- text-embedding-3-small/large
- Vector search
- Semantic similarity
- Clustering

### Image Generation
- DALL-E 3
- Dalle-2
- Image editing
- Variations

### Audio
- Whisper (speech-to-text)
- TTS (text-to-speech)
- Realtime audio

### Moderation
- Content filtering
- Safety checks
- Custom policies

## Boas Praticas

### Prompt Engineering
- Seja especifico e claro
- Use few-shot examples
- Chain-of-thought para raciocinio
- Output format especificado
- Temperature apropriada (0 para factual, 0.7-1 para criativo)

### Error Handling
- Retry com exponential backoff
- Rate limiting (429 errors)
- Timeout handling
- Fallback models
- Logging estruturado

### Cost Optimization
- Cache de responses
- Model selection (GPT-3.5 vs GPT-4)
- Token counting antes de enviar
- Streaming para responses longas
- Batching quando possivel

### Security
- Nunca expor API keys no frontend
- Validar user input
- Sanitizar outputs
- Rate limiting por usuario
- Audit logs

## Testing
- Mock OpenAI client
- Testar logica de negocios
- Edge cases
- Calls reais para API (com test keys)
- End-to-end workflows
- Performance benchmarks

## Monitoring
- Latencia (p50, p95, p99)
- Token usage
- Error rates
- Cost per request
- OpenTelemetry
- LangSmith
- Weights & Biases