# Publication readiness

Lifecycle canônico: `DRAFT → VALIDATING → READY_TO_SYNC → REQUESTED → PREPARING → SYNCING → PUBLISHED`.

Estados auxiliares incluem `WAITING_BACKOFFICE`, `FAILED` e estados stale. `DRAFT` é edição; `VALIDATING` executa diagnóstico; `READY_TO_SYNC` é preflight aprovado; `REQUESTED` é intenção idempotente; `PREPARING` monta o draft; `SYNCING` chama o destino; `PUBLISHED` exige resultado persistido e confirmado. `WAITING_BACKOFFICE` bloqueia até correção interna. `FAILED` diferencia falha temporária de definitiva e não reabre histórico automaticamente.

O preflight usa `validateListing()` e `computeValidationDecision()`; preservação de status usa `publicationStatusForValidation()` e a persistência canônica é `MarketplaceListingRepository::updateValidation()`. Só então `MarketplacePublicationPreparationService` pode preparar e `MarketplaceSyncQueueService` pode enfileirar. Requests/jobs são criados ou reutilizados idempotentemente por tenant, seller, listing e marketplace.

Estados stale devem ser reconciliados pela validação canônica antes de nova ação. Uma nova ação é avaliada pelo estado atual; não execute retry operacional durante uma etapa que só corrige configuração. Nenhum job ou chamada externa existe antes do preflight aprovado. Após sincronizar, releia o estado persistido e reconcilie o remoto.
