---
name: otimizacao-performance
description: Otimização de performance do ISAC Conecta — React, consultas Supabase e custo/latência do motor de IA. Aplique quando algo estiver lento, quando a vitrice carregar muitos anúncios, quando a conta da API de IA preocupar, ou quando pedirem para "deixar mais rápido/leve". Regra de ouro: meça antes de otimizar.
---

# Otimização de performance

Meça antes de mexer. Otimizar no achismo gera código complicado sem ganho. Só otimize o que
um número mostrou ser lento.

## Front-end (React)
- **Lista da vitrine:** pagine ou virtualize. Não renderize 500 cards de uma vez.
- **Re-render:** `useMemo`/`useCallback` só onde há custo real; `React.memo` em card de lista.
- **Carregamento:** `lazy` + `Suspense` para telas de Nível 2 (área comercial, painel) que
  nem todo usuário abre.
- **Imagem:** tamanho certo, `loading="lazy"`, sem asset gigante.
- **Não busque no render:** dados via hook/serviço, com cache simples de sessão.

## Banco (Supabase / PostgreSQL)
- **`select` só das colunas que usa** — nunca `select *` na vitrine.
- **Índice** nas colunas de filtro/ordenção (`categoria`, `status`, `criado_em`).
- **Paginação** (range/limit) sempre; nunca traga a tabela inteira.
- **Sem N+1:** para métricas do painel, use `view`/agregação, não um loop de queries.

## Motor de IA (custo e latência — o único custo variável do MVP)
- **Cache por hash do texto:** mensagem repetida não re-chama a IA.
- **Batch:** na demonstração, processe a lista colada de uma vez, não 1 a 1.
- **Limiar/pré-filtro:** descarte "bom dia" e correntes com regra barata antes de gastar token.
- **Timeout** para não pendurar a tela esperando o LLM.
- **Modelo certo:** o menor modelo que resolve a classificação — não o mais caro por hábito.

## Como medir
- Front: aba Performance / Network do navegador; React DevTools Profiler.
- Banco: `explain analyze` na query suspeita.
- IA: registre latência e tokens por chamada (casa com `prompt-ops`).

## Ordem de prioridade
1. Custo da IA (dinheiro real). 2. Fluxo Publicar→Vitrice (o que aparece na demo).
3. O resto. Não gaste tempo otimizando tela que ninguém abre na apresentação.
