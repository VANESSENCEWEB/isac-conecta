---
name: convencoes-do-projeto
description: Convenções de código e entrega do ISAC Conecta — nomes, estrutura de pastas, tokens de CSS, mobile-first e formato de entrega. Aplique SEMPRE que criar arquivo novo, nomear função/tabela/componente, escrever estilo, ou decidir onde algo mora. Garante que 8 pessoas produzam código que parece escrito pela mesma mão.
---

# Convenções do projeto

O objetivo é que o código de 8 pessoas leia como se fosse de uma só. Siga sem exceção.

## Idioma
- Domínio em **pt-BR**: `anuncios`, `perfis`, `publicarAnuncio`, `categoria`. O produto é de
  bairro brasileiro; o código fala a língua do domínio.
- Termos técnicos consagrados podem ficar em inglês (`status`, `id`, `props`).

## Nomes
- **Banco:** `snake_case` (`autor_id`, `criado_em`, `fatia_isac`).
- **JS/TS:** `camelCase` para função/variável, `PascalCase` para componente React.
- **Arquivo de componente:** `Card.tsx`, `BarraImpacto.tsx`. Serviço: `anuncios.ts`.
- Nome diz o que faz. `dados`, `x`, `temp`, `handleClick2` não passam em review.

## Estrutura (segue a arquitetura)
```
frontend/src/{paginas, componentes, servicos, estilos, hooks}
backend/{rotas, servicos, ia, modelos}
banco/            # migrações + RLS
```
Achou em dúvida onde algo mora? Pergunte ao agente `arquiteto-revisor`.

## CSS-variables-first
- Toda cor/espaço/fonte vem de token (`var(--primary)`, `var(--sp-4)`). **Nunca** hex cru no
  componente.
- Papéis semânticos fixos: `--primary`, `--accent`, `--ink`, `--page-bg`.
- **Mobile-first:** estilo base é o do celular; `min-width` só para subir.

## Formato de entrega (preferência da Vanessa)
- Entregue **arquivo completo e funcional**, não trecho solto que depende de "cole no lugar X".
- Solução prática e imediatamente usável ganha de elegância arquitetural que ninguém termina.
- Se o arquivo depende de config (env, migração), diga em uma linha o que rodar.

## Commits e branches
Ver skill `git-fluxo`.

## Regra final
Consistência > preferência pessoal. Se o projeto já faz de um jeito, faça igual, mesmo que
você faria diferente sozinho.
