# Hineni Mail — Projeto

## Objetivo

Oferecer e-mail corporativo gerenciado para pequenas empresas, com baixo custo recorrente, sobre o projeto open source [OpenInbox](https://github.com/sums001/OpenInbox) (MIT): Cloudflare Workers, D1, Email Routing e provedores externos de envio (Resend primário; Brevo alternativo).

## Estratégia

1. Um ambiente de laboratório interno serve de homologação.
2. Após aprovação técnica, a primeira cliente externa recebe uma instância própria.
3. Cada cliente tem **instância independente** em conta Cloudflare própria (ver `DECISIONS.md`).

## Estado atual

| Aspecto | Estado |
| --- | --- |
| Fork criado, baseline fixada | **Implementado** |
| Build, lint, typecheck, testes unitários/integração e e2e locais | **Validado** (ver `TEST-MATRIX.md`) |
| Migrations D1 em banco local descartável | **Validado** |
| Instância implantada na Cloudflare | **Não implantado** |
| Domínio delegado à Cloudflare | **Planejado** (plano privado) |
| Envio por Resend/Brevo | **Planejado** |
| R2 (anexos) | **Planejado** (obrigatório na homologação corporativa) |
| Conta Cloudflare exclusiva do laboratório | **Bloqueado** (aguarda Product Owner) |

## Princípios

- Preservar o upstream; customizações só por missão e ADR.
- Documentação pública sanitizada; documentação operacional privada.
- Nada de infraestrutura privada no caminho do e-mail.
- Uso responsável: conversas reais, sem marketing em massa nem cold outreach (política do upstream e dos provedores).

## Documentos

`ARCHITECTURE.md` · `ROADMAP.md` · `DECISIONS.md` · `SECURITY.md` · `TEST-MATRIX.md` · `DEPLOYMENT-RUNBOOK.md` · `BACKUP-RESTORE.md` · `COSTS.md` · `CHANGELOG.md`
