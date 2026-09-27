# Extensões futuras

Amazon, Shopee e outros canais devem ser adicionados como adaptadores, sem alterar o núcleo comum e sem transformar regras de um marketplace em regras globais.

Cada adaptador pode implementar capacidades de:

- categoria;
- atributos e valores permitidos;
- variações;
- montagem/validação de payload;
- cliente externo;
- erros e política de retry;
- autenticação;
- rate limit;
- reconciliação.

O núcleo fornece produto, SKU, readiness, idempotência, escopo e resultados. A capability matrix declara o que cada canal suporta. Amazon e Shopee não são implementados nesta versão; seus contratos, credenciais e IDs devem permanecer isolados até haver especificação própria.
