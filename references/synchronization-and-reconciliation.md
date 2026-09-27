# Sincronização e reconciliação

Sincronização manual é orientada ao produto. O backend calcula destinos, readiness e retry; a UI do Seller não recebe `request_id`, `job_id`, mapping técnico ou Size Grid técnica. O Seller vê estado, motivo seguro e ação como `Solicitar integração`.

`PublicationSyncController` aceita a intenção no escopo tenant/seller; `postSyncNow` consulta destinos por `configuredMarketplacesFromCategoryLinks`, cria ou reutiliza request/job idempotente e delega ao `MarketplaceSyncQueueService`. A chave operacional é tenant + seller + listing + marketplace. Nenhuma chamada ocorre sem preflight.

Atualizações de preço e estoque preservam SKU e origem interna, são idempotentes e mantêm falhas parciais por item. UPDATE de produto, descrição e estoque são responsabilidades separadas; descrição pode exigir GET/comparação/POST ou PUT próprio.

Importação e vinculação de item remoto devem rejeitar ambiguidade, vínculo de outro seller ou reutilização indevida. IDs User Product por SKU ficam separados de `marketplace_variation_id`; não use fallback silencioso ao item pai.

Após cada operação, releia o estado persistido e reconcilie com o remoto quando autorizado. Divergência, item ausente ou estado stale vira diagnóstico e nova decisão explícita, não retry infinito. Tenant, seller, produto, listing e marketplace devem estar presentes em toda consulta e mutação.
