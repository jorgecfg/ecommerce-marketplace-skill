# Extensões futuras

Amazon, Shopee e outros canais devem ser adicionados como adaptadores, sem alterar o núcleo comum e sem transformar regras de um marketplace em regras globais.

Cada adaptador deve encapsular capacidades de:

- categoria;
- atributos e valores permitidos;
- variações;
- montagem/validação de payload;
- cliente externo;
- erros e política de retry;
- autenticação;
- rate limit;
- reconciliação.

Também deve declarar limitações de publicação e atualização parcial, tradução e contratos de erro próprios. Não copie regras de Mercado Livre para Amazon ou Shopee sem validar o contrato específico do canal; nenhum desses adaptadores é implementado nesta entrega.

O núcleo fornece produto, SKU, readiness, idempotência, escopo e resultados. A capability matrix declara o que cada canal suporta. Amazon e Shopee não são implementados nesta versão; seus contratos, credenciais e IDs devem permanecer isolados até haver especificação própria.
