# Changelog (camada Hineni)

Registra apenas mudanças da Hineni sobre o upstream. O histórico do OpenInbox permanece no Git.

## Não lançado

### M02 — Segurança
- `fix(deps)`: Hono 4.13.13 → 4.13.22 (`package.json` e entrada do Hono no `package-lock.json`; nenhum outro pacote alterado). Auditoria de produção: 0 vulnerabilidades.
- `test(security)`: `test/integration/security-authz.test.ts` (8 testes de regressão de autorização/CSRF/variantes de caminho).
- Documentação: ADR-011, resultados de segurança e matriz de testes atualizada.
- Nenhuma alteração no código-fonte do Worker, em migrations, workflows ou `.gitignore`.

### M01 — Fundação do projeto
- Fork público criado a partir de `sums001/OpenInbox`; baseline fixada na tag `upstream-baseline-20261124` (SHA `d17801db0de3c1ddd17a932656f7947134048568`).
- Branch `hineni/develop` criada a partir da baseline; `main` mantida como espelho do upstream.
- GitHub Actions desabilitado nas configurações do fork.
- Adicionados `CLAUDE.md` e `docs/hineni/*`.
- **Nenhuma alteração** no código-fonte do OpenInbox, nas migrations, nos workflows ou no lockfile.
