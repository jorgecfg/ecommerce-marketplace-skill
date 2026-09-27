# Núcleo de domínio

O núcleo é neutro a marketplace e não assume campos, IDs ou APIs de um canal. O produto interno é a fonte de verdade; o adaptador traduz para um destino externo.

- **Produto:** entidade interna comercial, pertencente a um tenant; contém identidade, título, descrição, imagens e referências a SKUs.
- **SKU:** unidade vendável com identificador interno, preço, estoque disponível, imagens e dimensões próprias.
- **Variação:** combinação de atributos vendáveis que aponta para SKU(s), sem confundir ID interno com ID remoto.
- **Preço e estoque:** dados comerciais internos; preço resolvido e saldo disponível devem ser transportados explicitamente, sem inferir de outro SKU.
- **Imagem e descrição:** conteúdo interno versionável, sujeito às regras do destino e, quando necessário, a fluxo de atualização separado.
- **Categoria interna:** classificação canônica do catálogo, distinta da categoria externa de cada canal.
- **Atributo interno:** campo e valor do catálogo, com tipo, origem e regras de validação.
- **Mapeamento externo:** relação explícita e versionada entre entidade interna e campo/valor/categoria remotos. Ambiguidade permanece ambígua e pendente; texto livre nunca é chave.
- **Listing:** vínculo interno entre produto/destino e o ciclo de publicação.
- **Item remoto:** referência externa persistida separadamente do listing e do ID da variação.
- **Destino de publicação:** tenant, seller, marketplace e categoria remota sob os quais uma publicação é feita.
- **Readiness:** estado persistido que diz se o destino pode avançar no ciclo de publicação.
- **Resultado de publicação:** evidência persistida de sucesso, falha, IDs remotos, mensagens sanitizadas e possibilidade de retry.

IDs internos são a referência técnica. O Seller não configura estruturas técnicas globais: políticas, mapeamentos e decisões ficam no backend/service/policy; configuração de categoria, atributo, valor e produto permanece separada. Toda operação deve ser tenant/seller-scoped, repetível com idempotency key e auditável.
