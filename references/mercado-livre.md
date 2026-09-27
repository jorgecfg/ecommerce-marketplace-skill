# Mercado Livre

## Preparação e preflight

Carregue produto, SKUs, preços, estoque, imagens, descrição, categoria interna, mapeamentos e destino no escopo do tenant e seller. Resolva a categoria Mercado Livre e valide atributos obrigatórios, permitidos e seus valores. Não selecione um mapeamento quando houver conflito.

Normalize variações: cada combinação deve ser única, completa e ligada ao SKU correto. Preserve preço e estoque por SKU; nunca use o preço de outra variação como fallback silencioso. Valide imagens acessíveis, formatos/tamanhos aceitos e descrição sanitizada.

## Payload e operações

Monte o payload a partir do snapshot validado: categoria, título, atributos, variações, preços, estoque, imagens, descrição e configurações de envio aplicáveis. IDs externos só podem vir de mapeamentos ou respostas reais do Mercado Livre.

Na publicação, respeite a readiness e registre request, payload sanitizado e resultado. Na atualização, envie apenas mudanças válidas e idempotentes. Sincronizações devem manter o seller e o produto de origem, com resolução explícita do item remoto.

## Reconciliação e retries

Após uma operação, releia o estado persistido e reconcilie com o remoto quando permitido. Não trate ausência de exceção como sucesso. Faça retry apenas para rate limit, timeout ou erro temporário, com backoff e idempotência; erros de contrato e validação exigem correção.
