# Browser Automation for AI - Automação de Navegador para IA

## O que e
Permitir que agentes de IA interajam com interfaces web como um humano faria, para tarefas que não possuem API.

## Ferramentas
- Playwright ou Puppeteer controlados por LLM (ex: Browser Use, AgentQL)
- Modelos de visão (GPT-4V) para entender a UI e identificar elementos clicáveis
- DOM tree simplificado para o LLM entender a estrutura da página

## Padrões
- Observação: Agente tira screenshot e lê o DOM
- Planejamento: Agente decide qual elemento interagir
- Ação: Agente clica, digita ou rola a página
- Validação: Agente verifica se a ação teve o efeito esperado

## Desafios
- Sites com CAPTCHA ou proteções anti-bot (requer proxies residenciais ou serviços de bypass)
- Mudanças frequentes no layout do site (requer robustez na seleção de elementos)
