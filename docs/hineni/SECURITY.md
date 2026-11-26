# Segurança

Este documento é público e sanitizado. Detalhes operacionais ficam em registros privados.

## Princípios

- Secrets nunca entram no repositório (`.dev.vars`, `.wrangler/` e credenciais são ignorados pelo Git).
- Testes usam dados fictícios e APIs mockadas; nenhuma chamada autenticada a provedores reais.
- Sem deploy, DNS ou envio real sem missão autorizada.
- GitHub Actions desligado no fork até decisão expressa.
- O upstream é beta; a baseline é fixada por SHA e atualizações são manuais.

## Auditoria de dependências na baseline

`npm audit` foi executado em modo de diagnóstico, **sem aplicar correções**. Resultado na baseline: 16 advisories (3 altos, 13 moderados; nenhum crítico). Apenas 1 afeta dependência de produção (framework HTTP do Worker, versão corrigida disponível em patch). Os demais estão em dependências de desenvolvimento/teste.

- Ausência de explorabilidade comprovada **não** é prova de segurança, e a presença de advisories não significa exploração.
- A análise de impacto e a atualização controlada são trabalho de missão futura (ver `ROADMAP.md`).
- Detalhamento por pacote fica no relatório privado da missão.

## Reporte de vulnerabilidades

Para problemas na camada Hineni, contate o Product Owner pelos canais da Hineni Digital. Para o código upstream, use os canais do projeto OpenInbox.

## Uso responsável

Conforme política do upstream e dos provedores de envio: conversas reais, sem spam, sem marketing em massa e sem contornar limites com múltiplas contas gratuitas.
