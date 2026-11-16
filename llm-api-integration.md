# LLM API Integration

## Provedores
- OpenAI: GPT-4, GPT-3.5, embeddings, TTS, Whisper
- Anthropic: Claude 3 (Opus, Sonnet, Haiku)
- OpenRouter: Roteador para multiplos modelos com melhor custo
- Local: Ollama, vLLM para privacidade e custo zero

## Padroes de Integracao
- Retry com exponential backoff para erros 429/5xx
- Timeout configuravel para requisicoes longas
- Fallback para modelo menor se o principal falhar

## Seguranca
- Nunca expor API keys no frontend
- Usar variaveis de ambiente ou secret managers (AWS Secrets, Vault)
- Rate limiting por usuario/IP no backend