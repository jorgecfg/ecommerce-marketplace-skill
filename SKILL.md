---
name: ecommerce-marketplace-skill
description: Especialista em cadastro, validação, publicação e sincronização de produtos no Mercado Livre, incluindo variações e Size Grid.
---

# Ecommerce Marketplace

Use esta skill para orientar fluxos de catálogo e publicação no Mercado Livre. A versão atual documenta e suporta apenas Mercado Livre; Amazon e Shopee aparecem somente como extensões arquiteturais.

## Princípios

- Preserve `tenant_id`, seller, escopo e idempotência em toda operação.
- Mantenha produto interno, SKU, variação, listing e IDs externos semanticamente separados.
- Nunca fabrique, adivinhe ou derive IDs externos. Isso inclui `SIZE_GRID_ID` e `SIZE_GRID_ROW_ID`.
- Faça preflight completo antes de qualquer chamada externa. Se houver pendência, bloqueie a publicação e informe o motivo acionável.
- Não exponha credenciais, tokens, cookies ou dados reais de sellers.
- Diferencie proposta, validação, publicação, atualização e reconciliação.

## Fluxo acionável

1. Carregue o contexto do produto no tenant e seller corretos.
2. Valide categoria, atributos, SKUs, variações, preço, estoque, imagens e descrição.
3. Normalize combinações de variação e resolva mapeamentos externos sem inferência.
4. Quando aplicável, execute o fluxo de Size Grid em [references/mercado-livre-size-grid.md](references/mercado-livre-size-grid.md).
5. Monte e valide o payload específico do Mercado Livre.
6. Só avance para publicação quando o preflight estiver aprovado e a readiness permitir.
7. Persista o resultado, faça reconciliação e use retry somente para falhas recuperáveis.

Consulte [references/core-domain.md](references/core-domain.md) para o núcleo neutro, [references/mercado-livre.md](references/mercado-livre.md) para o adaptador atual, [references/mercado-livre-errors.md](references/mercado-livre-errors.md) para tratamento de falhas e [references/publication-readiness.md](references/publication-readiness.md) para estados. A extensão de novos canais está em [references/future-marketplaces.md](references/future-marketplaces.md).
