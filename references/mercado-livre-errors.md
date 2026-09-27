# Erros do Mercado Livre

| Erro | Causa/camada; decisão |
|---|---|
| `VARIATION_DIFFERENTIATOR_NOT_FOUND` | Variação sem diferenciador; normalizador; bloqueia preflight, sem retry |
| `VARIATION_ATTRIBUTE_MAPPING_MISSING` | Mapeamento obrigatório; configuração; bloqueia, Backoffice, sem retry |
| `VARIATION_ATTRIBUTE_NOT_ALLOWED_FOR_CATEGORY` | Contrato de categoria; adaptador; bloqueia, corrigir produto/policy |
| `SIZE_GRID_ID_NOT_CONFIGURED_TECHNICAL` | Grid não resolvida; Service/policy; bloqueia, recuperação/Backoffice |
| `SIZE_GRID_RECONCILE_INCOMPLETE` | Reconciliação de linhas incompleta; Service; bloqueia e exige reconciliação |
| Categoria/atributo obrigatório ausente | Preflight; completar produto ou mapping; sem POST |
| Combinação duplicada/valor ausente | Normalização; bloqueia até correção; sem retry |
| Token expirado | Autenticação; renovar conexão, retry só após correção |
| Rate limit/timeout/erro temporário | Cliente externo; retry idempotente com backoff e limite |
| Erro parcial | Orquestração; persistir por SKU/item e reconciliar, não repetir tudo cegamente |
| Item remoto divergente | Reconciliação; rejeitar ambiguidade, revisar vínculo; sem fallback |
| UPDATE sem alteração efetiva | Changeset/cliente; confirmar remoto e marcar no-op; não enviar UPDATE vazio |
| Erro definitivo | Contrato externo; falha final, ação explícita; não reabrir histórico |

Para cada erro, registre causa provável, camada, bloqueio, retry/reconciliação e decisão de Backoffice. A mensagem do Seller deve ser segura e acionável; logs internos podem conter diagnóstico sanitizado, nunca tokens, cookies ou dados privados.
