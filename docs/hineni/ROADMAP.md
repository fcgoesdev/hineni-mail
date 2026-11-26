# Roadmap

Legenda: **Implementado** · **Validado** · **Planejado** · **Bloqueado**

| Missão | Escopo | Estado |
| --- | --- | --- |
| M00 | Discovery e inventário somente leitura | Implementado |
| M01 | Baseline Git, fundação, testes locais, documentação, plano de DNS | Implementado; ver `CHANGELOG.md` |
| M02 | Fundação de segurança (Hono, regressão de autorização) e fundação Cloudflare (zona de laboratório) | Segurança: implementada e validada localmente. Cloudflare: em andamento (delegação DNS pendente) |
| M03 | A definir pelo orquestrador | Planejado |

## Itens candidatos (sujeitos a missão e autorização)

- Atualização controlada de dependências com advisories (revisar impacto e testes) — **Planejado**
- Conta Cloudflare exclusiva do laboratório e primeiro deploy de homologação — **Bloqueado** (aguarda conta e autenticação)
- Delegação de DNS do domínio do laboratório à Cloudflare, com tratamento de DNSSEC — **Planejado** (plano privado)
- Provedor de envio primário (Resend) e alternativo (Brevo) — **Planejado**
- R2 para anexos — **Planejado**
- Backup e restauração testados do D1 — **Planejado**
- Primeira cliente externa — **Planejado**, só após aprovação técnica do laboratório
