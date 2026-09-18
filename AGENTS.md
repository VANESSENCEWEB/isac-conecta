# AGENTS.md — Leia isto primeiro

> Este arquivo é a **porta de entrada para qualquer IA** (Claude, Cursor, Copilot, ChatGPT…)
> e para qualquer pessoa do grupo. Se você é uma IA trabalhando neste repositório, **comece
> por aqui** e siga a ordem abaixo antes de escrever qualquer linha de código.

## O que é o ISAC Conecta
Plataforma web que usa IA para transformar o caos dos grupos de WhatsApp na **economia
organizada do bairro**, gerando receita recorrente que sustenta o ISAC (meta ~R$ 2.000/mês).
Fluxo-coração: mensagem bruta → IA classifica e extrai (categoria, preço, contato) → card
estruturado → vitrine pesquisável. Projeto integrador GrowUp/Porto Digital · entrega 02/out/2026.

## Regra de ouro (para qualquer IA)
1. **Leia** `docs/dev-kit/ARQUITETURA.md` — camadas, fronteiras e o contrato central.
2. **Escolha o agente** da frente que você vai tocar em `docs/dev-kit/agentes/` e carregue-o.
3. **Aplique as skills** transversais de `docs/dev-kit/skills/` (segurança e convenções são
   obrigatórias em tudo).
4. **Respeite as fronteiras.** Não misture frentes; cada agente é um contexto isolado.
5. **Documente.** Ao fim de uma atividade relevante, registre em `docs/relatorios/` (ver abaixo).
6. **Idioma:** tudo em **pt-BR** (domínio, commits, comentários, relatórios).

## Mapa do repositório
```
isac-conecta/
├── README.md                    # porta de entrada humana (como rodar o projeto)
├── AGENTS.md                    # ESTE arquivo — porta de entrada para IA
├── CLAUDE.md                    # atalho p/ Claude Code → aponta para AGENTS.md
├── .gitignore
│
├── frontend/                    # React (web responsivo)
│   └── src/{paginas, componentes, servicos, estilos, hooks}
├── backend/
│   ├── rotas/                   # endpoints — ponto de segurança
│   ├── servicos/                # regras de negócio
│   ├── ia/                      # ISOLA o LLM: prompts, parser, validação
│   └── modelos/                 # entidades do domínio
├── banco/                       # migrações SQL + políticas RLS
│
└── docs/                        # tudo que orienta o projeto
    ├── dev-kit/                 # como a IA e o time trabalham
    │   ├── README.md
    │   ├── ARQUITETURA.md       # ← contexto compartilhado, leitura obrigatória
    │   ├── agentes/             # 01..08 — um contexto por frente
    │   └── skills/              # segurança, convenções, performance, prompt-ops, git…
    ├── design-system/           # a identidade visual
    │   ├── tokens.css           # ← fonte da verdade de cor/tipo/espaço (Inter, base 4px)
    │   ├── 00-cover.png
    │   ├── 01-fundamentos.png
    │   ├── 02-iconografia-grid.png
    │   └── 03-tipografia-espacamento.png
    └── relatorios/              # diário de bordo do projeto
        ├── README.md
        ├── _modelo.md
        └── AAAA-MM-DD.md        # um por dia/atividade
```

## Qual agente usar
| Vou mexer em… | Agente |
|---|---|
| Estrutura, refactor, "onde isso mora", integração entre frentes | `01-arquiteto-revisor` |
| Extrair/classificar mensagem, prompt do LLM, parser | `02-motor-ia` |
| Banco, schema, RLS, auth, serviços, endpoints | `03-backend-supabase` |
| Telas, componentes, formulários, busca/filtro | `04-frontend-react` |
| Cor, tipografia, espaçamento, tokens, responsivo | `05-design-ui` |
| Pagamento Pix, área do comércio (Nível 2) | `06-pagamentos-comercio` |
| Painel de impacto, métricas (Nível 2) | `07-painel-isac` |
| Teste, bug, "não funciona", véspera da entrega | `08-qa-testes-debug` |

## Não-negociáveis (valem para toda IA e toda pessoa)
- **Segurança:** valida entrada, RLS em toda tabela, erro/log sem vazar segredo. Ver
  `skills/seguranca-por-design`.
- **Contrato:** o card `AnuncioEstruturado` (seção 5 da arquitetura) é o formato comum.
- **Fronteira da IA:** só `backend/ia` fala com o LLM. Tela nunca chama IA nem monta SQL.
- **Design:** cor/tipo/espaço só via `docs/design-system/tokens.css`. Sem hex/px cru.
- **Convenções:** `skills/convencoes-do-projeto` (nomes em pt, mobile-first, arquivo completo).

## Como uma IA "entra" no projeto na prática
- **Claude Code / editor com agentes:** os `.md` de `docs/dev-kit/agentes/` podem ir também em
  `.claude/agents/` e as skills em `.claude/skills/` — já estão no formato certo.
- **Qualquer outro chat de IA:** cole no início da conversa **dois** arquivos —
  `docs/dev-kit/ARQUITETURA.md` + o agente da frente. Isso dá o contexto exato, sem poluir.

## Diário de bordo (obrigatório)
A cada dia trabalhado ou atividade concluída, crie/atualize `docs/relatorios/AAAA-MM-DD.md`
a partir de `docs/relatorios/_modelo.md`. Isso alimenta o **Bloco 5 (Relato do processo)** da
entrega — documentar não é burocracia, é nota.
