# Registro de decisões (ADR)

| ID | Decisão | Estado |
| --- | --- | --- |
| ADR-001 | Conta Cloudflare exclusiva por ambiente (laboratório tem conta própria) | Aprovada; conta ainda não criada |
| ADR-002 | Instâncias independentes por cliente | Aprovada |
| ADR-003 | Baseline fixada no commit `d17801db0de3c1ddd17a932656f7947134048568` (tag `upstream-baseline-20261124`); sem avançar para commit mais recente sem autorização | Implementada |
| ADR-004 | Fork público `fcgoesdev/hineni-mail` | Implementada |
| ADR-005 | Preservar o código upstream, sem customizações funcionais na M01 | Implementada |
| ADR-006 | Node.js 24 preferencial, para reproduzir o CI upstream | Implementada (via gerenciador de versões, sem tocar no Node global) |
| ADR-007 | R2 obrigatório para homologação corporativa | Aprovada; não implantado |
| ADR-008 | Resend primário; Brevo alternativa a homologar | Aprovada; não configurado |
| ADR-009 | Documentação pública sanitizada no GitHub; documentação operacional privada | Implementada |
| ADR-010 | Servidores privados e ferramentas de automação não são dependência do fluxo de e-mail | Aprovada |
| ADR-011 | Atualizações de segurança em dependências devem ser pontuais, reproduzíveis e acompanhadas por testes de regressão | Aprovada; aplicada na M02 (Hono) |

## Decisões operacionais da M01

- **GitHub Actions desligado no fork.** O fork herda workflows de CI e de sincronização com o upstream. Para impedir qualquer execução remota involuntária, Actions foi desabilitado nas configurações do repositório. Reabilitar exige missão própria. (Os workflows não foram modificados.)
- **`.gitignore` do upstream não foi alterado.** Ele ignora `docs/` e `CLAUDE.md`; os arquivos da camada Hineni são versionados com `git add -f` por arquivo. Risco: novos arquivos em `docs/hineni/` ficam fora do `git status` até serem adicionados à força.
- **Pré-requisito de licença:** `LICENSE` (MIT) e autoria upstream preservadas.
