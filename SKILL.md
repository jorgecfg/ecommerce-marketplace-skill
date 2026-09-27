---
name: ecommerce-marketplace-skill
description: Especialista em cadastro, validação, publicação e sincronização de produtos no Mercado Livre, incluindo variações e Size Grid.
---

# Ecommerce Marketplace

Use esta skill para orientar decisões seguras de catálogo e publicação. Identifique o marketplace solicitado; Mercado Livre é o especialista suportado nesta versão. Amazon e Shopee aparecem somente como extensões arquiteturais.

## Princípios

- Preserve `tenant_id`, seller, escopo e idempotência em toda operação.
- Mantenha produto interno, SKU, variação, listing e IDs externos semanticamente separados.
- Nunca fabrique, adivinhe ou derive IDs externos. Isso inclui `SIZE_GRID_ID` e `SIZE_GRID_ROW_ID`.
- Faça preflight completo antes de qualquer chamada externa. Se houver pendência, bloqueie a publicação e informe o motivo acionável.
- Não exponha credenciais, tokens, cookies ou dados reais de sellers.
- Diferencie proposta, validação, publicação, atualização e reconciliação.
- O produto interno é a fonte de verdade; o marketplace é um destino externo. Traduza no adaptador/builder, sem acoplar o núcleo a nomes ou IDs do canal.
- Separe regras confirmadas, hipóteses e pontos dependentes de Backoffice. Não invente comportamento.
- Não exponha ao Seller request/job IDs, mappings técnicos, Size Grid ou detalhes internos; comunique uma ação segura e acionável.

## Fluxo acionável

Produto interno → diagnóstico do catálogo → validação de categoria e atributos → normalização de variações → resolução de Size Grid → construção do draft → preflight/readiness → publicação → persistência de referências externas → sincronização e reconciliação.

1. Carregue o contexto no tenant e seller corretos e confirme o modo do destino.
2. Valide categoria, atributos, SKUs, preço, estoque, imagens, descrição e conexão.
3. Normalize combinações e resolva mapeamentos externos sem inferência.
4. Quando aplicável, execute o fluxo de Size Grid em [references/mercado-livre-size-grid.md](references/mercado-livre-size-grid.md).
5. Monte e valide o draft específico do Mercado Livre.
6. Só avance quando o preflight estiver aprovado; qualquer bloqueio impede job e POST externo.
7. Persista o resultado, reconcilie e use retry somente para falhas recuperáveis.

Consulte [references/core-domain.md](references/core-domain.md), [references/mercado-livre.md](references/mercado-livre.md), [references/mercado-livre-size-grid.md](references/mercado-livre-size-grid.md), [references/publication-readiness.md](references/publication-readiness.md), [references/synchronization-and-reconciliation.md](references/synchronization-and-reconciliation.md) e [references/mercado-livre-errors.md](references/mercado-livre-errors.md). A extensão de novos canais está em [references/future-marketplaces.md](references/future-marketplaces.md).
