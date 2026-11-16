# Tool Use - Uso de Ferramentas por Agentes

## O que e
Agentes de IA usando ferramentas externas para expandir capacidades.

## Tipos de Ferramentas

### Search
- Web search (Google, Bing)
- Database search
- Document search

### Calculation
- Calculadoras
- Wolfram Alpha
- Python code execution

### APIs
- REST APIs
- GraphQL
- Webhooks

### File Operations
- Read/write files
- Parse documents
- Image processing

### Browser Automation
- Selenium
- Playwright
- Puppeteer

## Implementacao

### LangChain Tools
from langchain.tools import Tool
from langchain.utilities import GoogleSearchAPIWrapper

search = GoogleSearchAPIWrapper()

tool = Tool(
    name='Google Search',
    func=search.run,
    description='Use for searching the web'
)

tools = [tool]

### OpenAI Function Calling
functions = [
    {
        'name': 'get_weather',
        'description': 'Get current weather for a location',
        'parameters': {
            'type': 'object',
            'properties': {
                'location': {
                    'type': 'string',
                    'description': 'City name'
                }
            },
            'required': ['location']
        }
    }
]

response = openai.ChatCompletion.create(
    model='gpt-4',
    messages=[{'role': 'user', 'content': 'What is the weather in NYC?'}],
    functions=functions,
    function_call='auto'
)

### Custom Tool
def calculate(expression: str) -> str:
    try:
        result = eval(expression)
        return str(result)
    except:
        return 'Error'

calculator = Tool(
    name='Calculator',
    func=calculate,
    description='Use for mathematical calculations'
)

## Decision Making

### When to Use Tools
- Tarefa requer informacao atualizada
- Calculo complexo necessario
- Acesso a dados externos
- Acao no mundo real necessaria

### Tool Selection
- LLM decide qual tool usar
- Baseado em descricao da tool
- Contexto da conversa

### Fallback Strategy
- Se tool falha, tentar outra
- Ou responder sem tool
- Informar usuario do problema

## Best Practices

### Tool Descriptions
- Ser claro e especifico
- Incluir exemplos de uso
- Mencionar limitacoes

### Error Handling
- Catch exceptions
- Retornar mensagem de erro clara
- Log de erros

### Security
- Validar inputs
- Sandbox de execucao
- Rate limiting

### Performance
- Cache de resultados
- Timeout para chamadas
- Retry com backoff

## Exemplos de Uso

### Research Assistant
- Search web for information
- Read and summarize articles
- Cite sources

### Data Analyst
- Query databases
- Perform calculations
- Generate visualizations

### Customer Service
- Look up order status
- Process refunds
- Schedule appointments

## Trade-offs
- Latencia adicionada
- Dependencia de servicos externos
- Custo de API calls
- Complexidade de debugging

## Quando Usar
- LLM nao tem conhecimento suficiente
- Calculos precisos necessarios
- Acesso a dados em tempo real
- Acoes que requerem APIs externas