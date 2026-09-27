# Erros do Mercado Livre

| Erro | Tratamento |
|---|---|
| Mapeamento obrigatório ausente | Bloqueante; configurar mapeamento |
| Atributo não permitido | Corrigir payload/mapeamento; não fazer retry cego |
| Atributo obrigatório ausente | Bloqueante até completar o produto |
| Combinação duplicada | Bloqueante; normalizar variações |
| Valor de tamanho ausente | Bloqueante; completar SKU/atributo |
| Size Grid não configurada | Recuperável após configuração; sem chamada externa |
| Size Grid inconsistente | Recuperável após reconciliação; sem publicação parcial |
| Falha de autenticação | Corrigir conexão/credencial; não repetir indefinidamente |
| Rate limit | Retry com backoff e limite |
| Timeout | Retry idempotente e limitado |
| Erro temporário | Retry conforme política |
| Erro definitivo | Falha final, diagnóstico sanitizado e ação manual |

Registre código, operação, tenant/seller e correlação sem tokens, cookies ou payloads sensíveis.
