# Runbook de implantação

> **Estado: NÃO IMPLANTADO.** Este runbook é um esboço. Nenhum passo abaixo foi executado, e nenhum deve ser executado sem missão autorizada.

## Pré-requisitos (a cumprir antes de qualquer deploy)

1. Conta Cloudflare exclusiva do ambiente, autenticada, com método de pagamento se R2 for usado (ADR-007).
2. Domínio delegado à Cloudflare (plano privado, incluindo tratamento de DNSSEC).
3. Conta no provedor de envio primário e domínio verificado (ADR-008).
4. Candidata a release fixada por tag/SHA e com a matriz de testes aprovada.
5. Autorização expressa de missão para o deploy.

## Esboço (a detalhar em missão própria)

1. Criar o Worker e o D1 na conta do ambiente a partir da tag aprovada.
2. Abrir a página de setup, conectar o token Cloudflare (permissões mínimas) e **guardar a chave de recuperação** em gerenciador de senhas.
3. Conectar o domínio (Email Routing, SPF, DKIM, DMARC).
4. Configurar o provedor de envio em Admin → Integrações e habilitar R2.
5. Testes de recebimento e envio com endereços do próprio ambiente.
6. Registrar evidências sanitizadas.

## Atualizações

Manuais: analisar as notas da release upstream, testar em ambiente de homologação e só então atualizar. O Worker aplica migrations sozinho.

## Rollback

A definir. Depende de backup do D1 (ver `BACKUP-RESTORE.md`) e da versão anterior do Worker.
