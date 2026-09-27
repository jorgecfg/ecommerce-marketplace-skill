# Publication readiness

Estados normais:

`DRAFT → VALIDATING → READY_TO_SYNC → REQUESTED → PREPARING → SYNCING → PUBLISHED`

O preflight verifica escopo, autenticação disponível, categoria, atributos, variações, preço, estoque, imagens, descrição, Size Grid quando aplicável, idempotency key e ausência de conflitos. Só `READY_TO_SYNC` permite solicitar sincronização; só `PREPARING` aprovado permite chamada externa.

Transições devem ser persistidas, monotônicas dentro da operação e tenant/seller-scoped. `REQUESTED` não deve ser duplicado para a mesma intenção. Falhas recuperáveis retornam a estado retryável com backoff; falhas definitivas ficam `FAILED`/falha final e exigem nova ação explícita. Não reabra silenciosamente uma falha final.

Após publicar, confirme o resultado persistido e faça reconciliação. Se qualquer preflight falhar, não chame o marketplace: a evidência deve registrar o bloqueio e `external_post_called=false`.
