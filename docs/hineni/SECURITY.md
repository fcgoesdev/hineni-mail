# Segurança

Este documento é público e sanitizado. Detalhes operacionais ficam em registros privados.

## Princípios

- Secrets nunca entram no repositório (`.dev.vars`, `.wrangler/` e credenciais são ignorados pelo Git).
- Testes usam dados fictícios e APIs mockadas; nenhuma chamada autenticada a provedores reais.
- Sem deploy, DNS ou envio real sem missão autorizada.
- GitHub Actions desligado no fork até decisão expressa.
- O upstream é beta; a baseline é fixada por SHA e atualizações são manuais.

## Auditoria de dependências

**Baseline (M01):** `npm audit` em modo de diagnóstico, sem correções: 16 advisories (3 altos, 13 moderados; nenhum crítico). Apenas 1 afetava dependência de produção: o framework HTTP do Worker (Hono 4.13.13).

**Remediação (M02):** o Hono foi atualizado de 4.13.13 para **4.13.22** (linha 4.13.x, sem prerelease, pacote com procedência SLSA). Foram revisados todos os advisories publicados do Hono até 2026-11-26; a maior versão corretiva exigida por eles é 4.13.18, e a 4.13.22 inclui ainda endurecimentos posteriores. A mudança ficou restrita a `package.json` (uma linha) e à entrada do Hono no `package-lock.json`.

Resultado: `npm audit --omit=dev` → **0** vulnerabilidades. Restam 15 advisories (3 altos, 12 moderados) somente em ferramentas de desenvolvimento/teste (ex.: `undici` e `zod` aninhados em `miniflare`/`wrangler`/plugins de teste, `minimatch` na cadeia do ESLint); não entram no Worker implantado.

- O advisory GHSA-h7mg-cq63-vhpq (RegExpRouter ignorando middleware curinga) foi tratado como risco prioritário para exposição pública. Em testes locais, o roteador efetivamente ativo no Worker é o TrieRouter (o `SmartRouter` do Hono não adotou o RegExpRouter), e o defeito **não foi reproduzido** nem antes nem depois da atualização. Isso depende da tabela de rotas, então a atualização foi feita mesmo assim.
- Ausência de explorabilidade comprovada **não** é prova de segurança, e a presença de advisories não significa exploração.
- Atualizações de segurança seguem o ADR-011: pontuais, reproduzíveis (`npm ci`) e com testes de regressão.
- Os 15 advisories restantes em dependências de desenvolvimento ficam para missão futura, com atualização conjunta do ferramental da Cloudflare.

## Testes de autorização

`test/integration/security-authz.test.ts` cobre acesso anônimo, papéis (admin, membro), isolamento entre caixas, mensagens e anexos, permissão somente leitura, CSRF e variantes de caminho. Rodam em instância local descartável, com dados fictícios, a cada `npm test`.

## Reporte de vulnerabilidades

Para problemas na camada Hineni, contate o Product Owner pelos canais da Hineni Digital. Para o código upstream, use os canais do projeto OpenInbox.

## Uso responsável

Conforme política do upstream e dos provedores de envio: conversas reais, sem spam, sem marketing em massa e sem contornar limites com múltiplas contas gratuitas.
