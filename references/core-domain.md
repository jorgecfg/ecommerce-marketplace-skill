# Núcleo de domínio

O núcleo é neutro a marketplace e não assume campos ou APIs de um canal.

- **Produto:** entidade interna comercial, pertencente a um tenant; contém identidade, título, descrição, imagens e referências a SKUs.
- **SKU:** unidade vendável com identificador interno, preço, estoque e dimensões próprias.
- **Variação:** combinação de atributos vendáveis que aponta para um ou mais SKUs, sem confundir seu ID interno com o ID remoto.
- **Categoria interna:** classificação canônica do catálogo, distinta da categoria externa de cada canal.
- **Atributo interno:** campo e valor do catálogo, com tipo, origem e regras de validação.
- **Mapeamento externo:** relação explícita e versionada entre entidade interna e campo/valor/categoria remotos. Ambiguidade permanece pendente.
- **Destino de publicação:** tenant, seller, marketplace e categoria remota sob os quais uma publicação é feita.
- **Readiness:** estado persistido que diz se o destino pode avançar no ciclo de publicação.
- **Resultado de publicação:** evidência persistida de sucesso, falha, IDs remotos, mensagens sanitizadas e possibilidade de retry.

Toda operação deve ser tenant/seller-scoped, repetível com idempotency key e auditável.
