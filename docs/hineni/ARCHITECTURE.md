# Arquitetura

Descreve a arquitetura **do upstream no commit baseline** e as decisões da Hineni sobre ela. Nada aqui foi implantado.

## Componentes (upstream)

| Peça | Função |
| --- | --- |
| Cloudflare Email Routing | Recebe e-mail do domínio e entrega ao Worker (`email()` handler) |
| Worker único (Hono) | API, app web (assets estáticos, SPA), recebimento e jobs agendados |
| D1 | Caixas, mensagens, usuários, configurações, logs |
| Provedor de envio | Resend, Brevo, Mailjet, Cloudflare Email Sending ou SMTP, com fallback |
| R2 (opcional no upstream) | Anexos grandes, via API S3; **obrigatório** para homologação corporativa (ADR-007) |

Cron do Worker: a cada minuto (tarefas vencidas) e diário às 03:17 (manutenção).

## Migrations

O Worker aplica as próprias migrations no boot (`ensureMigrated`), usando a mesma tabela de controle do Wrangler (`d1_migrations`, por **nome completo** do arquivo). Ver auditoria resumida em `TEST-MATRIX.md`.

## Modelo de implantação Hineni

- Uma instância por cliente, em conta Cloudflare do cliente (ADR-001/002).
- Sem dependência de servidores privados ou ferramentas de automação no fluxo de e-mail (ADR-010).
- Fork público com código upstream preservado; documentação operacional fora do repositório.

## Fora de escopo agora

Customizações funcionais, multi-tenant em instância única, webhooks, API de inbox (itens de roadmap do upstream, ainda não disponíveis).
