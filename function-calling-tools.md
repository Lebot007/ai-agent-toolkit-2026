# Function Calling & Tools

## O que e
Permitir que o LLM chame funcoes externas para obter dados ou executar acoes.

## Implementacao
- Definir schema JSON das funcoes (nome, descricao, parametros)
- Enviar schema no prompt da API
- Parsear a resposta do LLM para identificar funcao e argumentos
- Executar funcao no backend e retornar resultado ao LLM

## Casos de Uso
- Busca na web em tempo real
- Consulta a banco de dados
- Calculadora ou execuçao de codigo Python
- Envio de email ou notificacao

## Frameworks
- LangChain Tools
- OpenAI Function Calling
- Anthropic Tool Use