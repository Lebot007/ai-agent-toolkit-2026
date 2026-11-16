# Accessibility (a11y) in AI Chat

## Principios WCAG
- Perceivable: Contraste de cores, texto alternativo para imagens
- Operable: Navegacao completa por teclado, foco visivel
- Understandable: Mensagens de erro claras, linguagem simples
- Robust: Compativel com screen readers (NVDA, VoiceOver)

## Implementacao
- ARIA labels para botoes de acao (copiar, regenerar)
- Live regions (aria-live) para anunciar novas mensagens da IA
- Skip links para pular navegacao
- Suporte a preferencia de reduced motion