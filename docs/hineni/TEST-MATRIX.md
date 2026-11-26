# Matriz de testes — baseline `d17801d`

Ambiente: Linux x86_64, Node.js 24.22.3, npm 11.19.1, Wrangler 4.151.3 (local, do lockfile). Instalação com `npm ci`. Tudo local: bindings D1 locais, APIs externas mockadas, nenhum deploy nem envio real.

| Verificação | Comando | Resultado | Observação |
| --- | --- | --- | --- |
| Instalação reproduzível | `npm ci` | PASS | `package-lock.json` inalterado (hash conferido) |
| Lint | `npm run lint` | PASS | |
| Typecheck | `npm run typecheck` | PASS | 4 projetos tsc |
| Testes unitários e integração | `npm test` | PASS | Baseline M01: 100 passaram, 1 ignorado. Após a atualização do Hono (M02): **108 passaram**, 1 ignorado (fixtures pesadas, condicional); 14 de 15 arquivos executados (+8 testes de autorização) |
| Autorização (regressão) | `test/integration/security-authz.test.ts` | PASS | 8 testes, executados antes (Hono 4.13.13) e depois (4.13.22) da atualização, ambos aprovados. Cobre: acesso anônimo, membro versus admin, isolamento entre caixas, mensagens e anexos, membro somente leitura sem envio, variantes de caminho (barras, segmentos de ponto, codificação, terminadores de linha) e CSRF |
| Cenários pesados | `npm run fixtures` + `test/integration/heavy.test.ts` | PASS (local, dados sintéticos) | 5 testes: newsletter de 500 KB, 40 imagens inline, anexo de 10 MB e mensagem de ~24 MB (perto do limite de 25 MB do Email Routing). Os arquivos são gerados localmente (não versionados) e removidos depois; sem eles o teste fica ignorado. **Item obrigatório da matriz de homologação** em ambiente real |
| Build | `npm run build` | PASS | |
| E2E (Playwright, Chromium) | `npm run test:e2e` | PASS | 1 passou, 1 ignorado (captura de screenshots do README, exige `OI_SCREENSHOTS=1`); repetido após a atualização do Hono |
| Smoke manual local (M02) | `npm run dev:mock` + `npm run dev`, `.dev.vars` fictício | PASS | Setup, login do administrador, navegação, criação de membro e caixa, controle de acesso (membro bloqueado nas rotas admin), recebimento simulado, envio simulado (provedor mock), logout (rotas privadas respondem 401). Processos encerrados e `.dev.vars` removido |
| Auditoria de dependências | `npm audit` / `npm audit --omit=dev` | Produção: **0**. Total: 15 (3 altos, 12 moderados), todos em ferramentas de desenvolvimento/teste | Sem `npm audit fix` |
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
