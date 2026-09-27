# Mercado Livre

Este é o adaptador suportado atualmente. O produto interno continua sendo a origem; nada abaixo deve virar regra global.

## Preparação e mapeamentos

Carregue tenant, seller, produto, listing anterior, conexão, modo (`MODE_USER_PRODUCT` ou Legacy), categoria interna e destino. Valide título e derive `family_name` sempre de `products.title`; não crie uma segunda fonte de verdade. Valide categoria Mercado Livre, atributos obrigatórios/permitidos, mapeamentos persistidos, imagens, descrição, SKU, preço e estoque.

Atributos internos são a origem. Traduza usando mapeamento persistido e valide ID e nome externo. Nunca escolha por semelhança textual, escreva valor de Seller em configuração global ou esconda conflito. Mapeamento obrigatório ausente bloqueia; categoria, atributo, valor e produto têm configuração separada.

## Variações e múltiplos SKUs

Normalize antes do payload: separe atributos de item e de variação, rejeite combinações duplicadas, valores ausentes e atributos não permitidos. `VARIATION_DIFFERENTIATOR_NOT_FOUND` é bloqueante. Preserve SKU, preço e estoque de cada combinação; use `SIZE_GRID_ROW_ID` somente com correspondência real e nunca fabrique-o. Quando o contrato exigir, não reintroduza `SIZE` em `attribute_combinations`.

No User Product, selecione pelo `seller_custom_field`, promova dados comerciais ao nível exigido, preserve `family_name` e o atributo raiz `COLOR`, remova `variations[]` quando o contrato exigir e faça fan-out por SKU. Cada SKU pode ter `marketplace_item_id` próprio; esse ID permanece separado de `marketplace_variation_id` e cada item remoto é atualizado individualmente. Em Legacy, preserve o contrato Legacy e não aplique silenciosamente o formato User Product.

## Preço, estoque e conteúdo

Resolva preço por variação a partir de `active_price`; não infira preço de outro SKU. Envie estoque disponível da fonte interna, sem confundir físico, reservado e disponível. Atualizações devem ser idempotentes; falhas parciais ficam persistidas e são reconciliadas.

Quando aplicável, descrição tem fluxo próprio: publique o item sem misturar responsabilidades, faça GET remoto, compare e execute POST/PUT específico apenas quando necessário. Suprima UPDATE vazio e reconcilie depois. Esse desenho é específico do Mercado Livre, não uma regra de outros canais.

## Publicação e atualização

Monte o draft com categoria, atributos, variações ou fan-out, preço, estoque, imagens e descrição. Passe pelo preflight/readiness antes de qualquer chamada. Persistir o resultado e reler o estado é obrigatório; ausência de exceção não prova sucesso.
