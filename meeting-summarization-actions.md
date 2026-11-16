# Meeting Summarization & Action Items - Resumos e Ações de Reuniões

## O que e
IA que participa de reuniões, transcreve, resume e extrai tarefas automaticamente.

## Arquitetura
- Integração com Zoom, Teams, Google Meet via bots ou plugins
- Pipeline: Áudio -> Whisper (STT) -> LLM (Sumarização) -> API de Tarefas (Jira/Notion)

## Padrões de Output
- Resumo executivo (3-5 bullet points)
- Tópicos discutidos com timestamps
- Action items com responsável e prazo (formato estruturado)

## Privacidade
- Consentimento explícito dos participantes para gravação
- Opção de desativar a IA para discussões confidenciais
- Criptografia de gravações em repouso
