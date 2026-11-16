# Code Review Automation - Automação de Code Review com IA

## O que e
Usar IA para realizar a primeira passada de revisão de código, liberando humanos para revisões de alto nível.

## Padrões
- Análise estática aprimorada por IA (além de ESLint/SonarQube)
- Detecção de padrões de anti-patterns e vulnerabilidades de segurança
- Sugestões de refatoração para legibilidade e performance

## Implementação
- GitHub App ou GitLab CI job que roda em cada PR
- Comentários inline no código com sugestões acionáveis
- Sumário do PR gerado automaticamente a partir dos commits

## Melhores Práticas
- Configurar regras estritas para não aprovar automaticamente
- Permitir que desenvolvedores marquem sugestões como "resolved" ou "ignored"
- Treinar o modelo com o style guide específico da empresa
