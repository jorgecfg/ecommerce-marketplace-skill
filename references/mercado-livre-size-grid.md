# Mercado Livre — Size Grid

1. Identifique, pela categoria Mercado Livre e sua política vigente, se a categoria exige ou permite Size Grid.
2. Resolva a grid aplicável por configuração/mapeamento explícito do tenant e seller. Valide categoria, gênero, atributos e conjunto de tamanhos.
3. Resolva `SIZE_GRID_ID` somente de uma configuração canônica ou resposta real do Mercado Livre.
4. Para cada tamanho, resolva o `SIZE_GRID_ROW_ID` real. A associação tamanho → SKU → linha deve ser completa, única e persistida.
5. Valide que todas as linhas usadas pertencem à grid resolvida e que não há tamanhos ausentes, duplicados ou incompatíveis.

Grid ausente, inconsistente, sem linha real ou com mapeamento ambíguo é bloqueante. O sistema deve marcar pendência recuperável quando for possível configurar/revalidar a grid, mas nunca publicar parcialmente.

Antes da chamada externa, o preflight deve comprovar aplicabilidade, `SIZE_GRID_ID`, todos os `SIZE_GRID_ROW_ID` e associações. Em qualquer falha, `external_post_called=false`. Nunca fabrique, incremente, derive pelo nome, copie de outro seller ou infira qualquer ID.
