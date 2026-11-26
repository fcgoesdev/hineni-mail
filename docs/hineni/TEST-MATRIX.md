# Matriz de testes — baseline `d17801d`

Ambiente: Linux x86_64, Node.js 24.22.3, npm 11.19.1, Wrangler 4.151.3 (local, do lockfile). Instalação com `npm ci`. Tudo local: bindings D1 locais, APIs externas mockadas, nenhum deploy nem envio real.

| Verificação | Comando | Resultado | Observação |
| --- | --- | --- | --- |
| Instalação reproduzível | `npm ci` | PASS | `package-lock.json` inalterado (hash conferido) |
| Lint | `npm run lint` | PASS | |
| Typecheck | `npm run typecheck` | PASS | 4 projetos tsc |
| Testes unitários e integração | `npm test` | PASS | 100 passaram, 1 ignorado (fixtures pesadas, condicional), 13 de 14 arquivos executados |
| Build | `npm run build` | PASS | |
| E2E (Playwright, Chromium) | `npm run test:e2e` | PASS | 1 passou, 1 ignorado (captura de screenshots do README, exige `OI_SCREENSHOTS=1`) |
| Migrations — banco vazio | `wrangler d1 migrations apply DB --local` | PASS | 8 migrations aplicadas |
| Migrations — reexecução | idem | PASS | "No migrations to apply" |
| Migrations — upgrade de estado anterior | aplicar 0001–0004_known_logins, depois o conjunto completo | PASS | esquema final idêntico ao do banco novo |
| Migrations — caminho do Worker | `test/integration/migrate.test.ts` (dentro do `npm test`) | PASS | |

## Auditoria das migrations 0004 duplicadas e lacuna 0005/0006

- O controle é feito pelo **nome completo** do arquivo (tabela `d1_migrations`), tanto pelo Worker quanto pelo Wrangler; o prefixo numérico serve apenas para ordenar. Ordem observada: `0004_known_logins`, `0004_totp_last_step`, `0007…`.
- As duas migrations `0004` são independentes (uma cria tabela, outra adiciona coluna) e foram aplicadas corretamente.
- `0005` e `0006` nunca existiram no histórico Git do upstream; a lacuna não gera risco observado.
- Risco residual: migrations futuras com prefixo duplicado ou fora de ordem. Mitigação: não renomear migrations existentes; revisar ordenação a cada atualização do upstream.

## Cobertura do fluxo local (e2e)

O teste e2e exercita: tela de setup, criação do administrador, integrações, domínios, usuários, assinatura, recebimento simulado, envio e resposta (provedores mockados), busca e isolamento entre membros. Não substitui teste em Cloudflare real.

## Pendente

- Teste em ambiente Cloudflare real — **Bloqueado** (conta não disponível).
- Envio real por Resend/Brevo — **Planejado**.
- Restauração de backup D1 — **Planejado**.
