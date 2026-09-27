# Mercado Livre — Size Grid / Fashion Grid

## Resolução

Identifique na categoria se a grid é necessária, aplicável, ausente ou inconsistente. Resolva a grid antes das combinações, usando `PublicationDraftService` e passando `resolvedSizeGrid` à resolução de variações. Construa `row_map` por correspondência real entre tamanho comercial, SKU e linha da grid.

Insira `SIZE_GRID_ID` somente quando vier de configuração canônica ou resposta real do Mercado Livre. Insira cada `SIZE_GRID_ROW_ID` somente quando a linha existir e pertencer à grid resolvida; mantenha-o em `variations[].attributes` quando o contrato exigir. Nunca fabrique, incremente, derive pelo nome, copie de outro seller ou infira IDs. Não restaure `SIZE` em `attribute_combinations` quando o contrato o remove.

## Decisão operacional

- **Recuperável:** configuração/reconciliação pendente que a policy autoriza recuperar automaticamente ou solicitar ao Backoffice.
- **Backoffice:** `SIZE_GRID_ID_NOT_CONFIGURED_TECHNICAL` ou configuração interna equivalente deve bloquear e orientar revisão interna, sem expor IDs ou detalhes técnicos ao Seller.
- **Bloqueante:** combinações duplicadas, valores ausentes, atributo não suportado, erro de policy, grid inconsistente, linha sem correspondência real e `SIZE_GRID_RECONCILE_INCOMPLETE`. Não suprima nem transforme em loop.

O Seller usa `Solicitar integração` quando o estado é interno; Size Grid não é wizard técnico. A policy fica no Service, o Repository apenas persiste e transições concorrentes usam CAS exato quando previsto. Em qualquer falha, bloqueie antes de POST externo e registre `external_post_called=false`.
