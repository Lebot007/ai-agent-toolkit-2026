# Collaborative Data Analysis - Análise de Dados Colaborativa com IA

## O que e
Ambientes onde analistas e IAs exploram datasets juntos, com a IA gerando queries e visualizações.

## Arquitetura
- Jupyter Notebooks ou ambientes similares com kernel de IA
- Text-to-SQL seguro com validação de schema
- Geração automática de gráficos (Matplotlib, Plotly, Vega-Lite)

## Padrões
- Humano faz pergunta em linguagem natural
- IA gera código SQL/Python e o executa em sandbox
- Humano valida o resultado e pede ajustes ("mostre como gráfico de barras")

## Segurança
- Sandboxing rigoroso para execução de código
- Somente acesso de leitura ao banco de dados de produção
- Masking de dados sensíveis (PII) antes da análise
