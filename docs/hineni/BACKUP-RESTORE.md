# Backup e restauração

> **Estado: PLANEJADO.** Nada foi implementado nem testado nesta fase, pois não existe instância implantada.

## O que precisa ser protegido

- Banco D1 (mensagens, usuários, configurações).
- Anexos no R2, quando habilitado.
- Chave de recuperação do proprietário e segredos do Worker (guardados em gerenciador de senhas, nunca no repositório).
- Configuração de DNS do domínio.

## A definir em missão futura

- Frequência e retenção de backups do D1 (ex.: exportação periódica e Time Travel do D1, a validar na documentação vigente da Cloudflare).
- Backup de objetos do R2.
- Procedimento de restauração e **teste de restauração periódico**, com critério de aceite.
- Armazenamento dos backups fora da conta que hospeda a instância.

Até que o procedimento seja testado, não se deve considerar que existe backup utilizável.
