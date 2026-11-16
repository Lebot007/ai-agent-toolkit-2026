# Anti-Block & Respectful Automation - Automação Respeitosa e Anti-Bloqueio

## O que e
Técnicas para garantir que automações e scrapers de IA não sejam bloqueados por WAFs (Web Application Firewalls) ou sistemas anti-bot, operando de forma ética e sustentável.

## Estratégias Legítimas
- Rate Limiting Respeitoso: Respeitar `robots.txt` e adicionar delays aleatórios entre requisições
- Rotação de Proxies: Usar pools de proxies residenciais ou datacenter de alta reputação
- User-Agent Rotation: Alternar entre User-Agents de navegadores reais e atualizados

## Técnicas Avançadas
- TLS Fingerprinting Spoofing: Usar bibliotecas como `curl_cffi` ou `tls-client` para imitar o handshake TLS de um navegador Chrome real
- Resolução de CAPTCHA: Integração ética com serviços de resolução (ou melhor, evitar páginas que exigem CAPTCHA para dados públicos)
- Browser Fingerprinting: Usar Playwright com plugins como `puppeteer-extra-plugin-stealth` para mascarar propriedades de automação

## Ética
- Sempre priorizar o uso de APIs oficiais quando disponíveis
- Não sobrecarregar servidores de pequenos proprietários
- Identificar o bot de forma transparente no User-Agent quando apropriado
