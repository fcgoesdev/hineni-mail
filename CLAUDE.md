# CLAUDE.md — Hineni Mail

Regras permanentes para agentes de código neste repositório. Valem para toda missão, salvo autorização expressa em contrário.

## O que é este repositório

Fork do [OpenInbox](https://github.com/sums001/OpenInbox) (MIT) usado pela Hineni Digital como base de e-mail corporativo gerenciado em Cloudflare Workers + D1. Contexto em `docs/hineni/PROJECT.md`.

- `main` espelha o upstream. **Nunca** commitar nele.
- `hineni/develop` é a linha de trabalho da Hineni.
- Baseline fixada: tag `upstream-baseline-20261124` (SHA `d17801db0de3c1ddd17a932656f7947134048568`).

## Governança por missão

1. O trabalho é dividido em missões numeradas (M01, M02, …) autorizadas pelo orquestrador/Product Owner.
2. Execute **somente** o escopo da missão autorizada. Não inicie a missão seguinte.
3. Se algo estiver bloqueado, continue as atividades independentes e registre o impedimento. Não contorne o bloqueio.
4. Não declare como verificado o que não foi verificado. Use os estados PASS / FAIL / BLOCKED / NOT VERIFIED / NOT APPLICABLE.
5. Relatórios operacionais completos ficam **fora** deste repositório, em diretório privado.

## Segurança (inegociável)

- Nunca expor, registrar ou commitar secrets, tokens, chaves, `.dev.vars`, dados locais do Wrangler (`.wrangler/`) ou credenciais.
- Este repositório é **público**. Não publicar: dados pessoais, informações de clientes, domínios reais de clientes ou do laboratório, hostnames privados, caminhos locais identificáveis, IDs de conta Cloudflare, relatórios operacionais completos.
- Sem deploy, sem `wrangler deploy`, sem `wrangler dev --remote`, sem migrations remotas, sem alterar DNS/DNSSEC, sem criar recursos Cloudflare, sem configurar provedores de envio, sem enviar e-mails reais — salvo missão que autorize isso expressamente.
- Testes usam apenas dados fictícios, bindings locais e APIs mockadas.
- Sem operações pagas sem autorização expressa.

## Código e dependências

- Preservar o código upstream. Mudanças funcionais só com missão específica e ADR registrado em `docs/hineni/DECISIONS.md`.
- Preservar `LICENSE` e a autoria upstream.
- Instalar com `npm ci` (lockfile existente). **Não** executar `npm update`, `npm audit fix` ou atualizações automáticas; correções de dependência exigem missão própria.
- Não editar nem renomear migrations existentes em `src/worker/db/migrations/`.
- Não forçar testes a passar alterando o código; diagnosticar e propor patch.
- Runtime preferido: Node.js 24 (mesmo do CI upstream), via gerenciador de versões; não alterar o Node global da máquina.
- Workflows de GitHub Actions não devem ser habilitados nem executados sem autorização (o fork mantém Actions desligado).

## Git

- Commits em `hineni/develop`, mensagens no estilo Conventional Commits.
- Sem force push, sem push em `main`, sem PR para o upstream sem autorização.
- O `.gitignore` do upstream ignora `docs/` e `CLAUDE.md`. Arquivos da camada Hineni nesses caminhos entram com `git add -f <arquivo>` (apenas eles; nunca `git add -f .`). O `.gitignore` não foi alterado, para manter o upstream intacto.
- Revisar `git status` e `git diff` completos antes de commitar; verificar ausência de secrets e dados privados nos arquivos staged.
- Nunca usar `rm -rf` em caminhos não criados pela própria missão, nem `git clean -fdx`.

## Comandos de validação (sequência do CI upstream)

```bash
npm ci
npm run lint
npm run typecheck
npm test
npm run build
npm run test:e2e   # requer: npx playwright install chromium
```
