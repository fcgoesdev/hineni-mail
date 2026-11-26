# Custos

> Valores publicados pelos fornecedores na data de consulta (2026-11-26) e sujeitos a mudança. Não há custo incorrido: nada foi implantado.

## Limites gratuitos relevantes

| Recurso | Limite gratuito |
| --- | --- |
| Cloudflare Worker (upstream) | 100.000 requisições/dia por conta |
| D1 | 500 MB de armazenamento |
| Mensagem recebida | até 25 MB |
| Resend (plano Free) | 100 e-mails/dia, 3 domínios |
| Brevo (plano Free) | 300 e-mails/dia (marketing e transacional somam) |
| Mailjet (citado pelo upstream) | 200 e-mails/dia |
| Cloudflare Email Sending | 3.000/mês, exige plano Workers Paid |
| R2 | 10 GB gratuitos, mas a conta precisa ter método de pagamento cadastrado |

## Pontos de atenção

- O cron a cada minuto consome requisições do Worker mesmo sem tráfego; medir no laboratório.
- R2 é obrigatório na homologação corporativa (ADR-007), logo o método de pagamento será necessário na conta.
- Os limites diários de envio são baixos para uso corporativo real; plano pago do provedor deve ser considerado antes de clientes em produção.
- Não contornar limites com múltiplas contas gratuitas: risco de suspensão e dano à reputação do domínio.
