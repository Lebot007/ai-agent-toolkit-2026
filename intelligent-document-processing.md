# Intelligent Document Processing (IDP) - Processamento Inteligente de Documentos

## O que e
Automação da extração, classificação e processamento de dados de documentos não estruturados ou semiestruturados.

## Pipeline
1. Ingestão: Receber PDF, imagem, email
2. Classificação: LLM ou modelo de visão identifica o tipo de documento (fatura, contrato, RG)
3. Extração: OCR + LLM extrai campos específicos (número da fatura, valor total, data)
4. Validação: Regras de negócio ou humano validam os dados extraídos
5. Integração: Dados estruturados são enviados para ERP/CRM via API

## Ferramentas
- AWS Textract, Google Document AI, Azure Form Recognizer
- Unstructured.io, LlamaParse para parsing avançado
- LLMs com capacidades de visão para documentos complexos

## Melhores Práticas
- Usar few-shot prompting com exemplos do formato específico do cliente
- Implementar confidence scores: se a confiança for baixa, enviar para revisão humana
