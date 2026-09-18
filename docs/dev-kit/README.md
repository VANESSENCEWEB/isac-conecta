# ISAC Conecta — Dev Kit (Agentes & Skills)

Pasta com os **agentes** e **skills** que otimizam, corrigem e mantêm o desenvolvimento do
ISAC Conecta coeso enquanto o grupo de 8 pessoas trabalha em paralelo até 02/out.

A ideia (que vem do teu prompt de arquiteto): **arquitetura primeiro**, depois o sistema é
decomposto em contextos isolados. Cada agente é um contexto autônomo — dá pra usar sozinho,
numa conversa nova com a IA, sem misturar/poluir o contexto de outra frente.

## Estrutura

```
isac-conecta-dev-kit/
├── ARQUITETURA.md          # contexto compartilhado — TODO agente começa lendo isto
├── agentes/                # um contexto isolado por frente de construção
│   ├── 01-arquiteto-revisor.md   # otimiza, corrige, guarda as fronteiras (o "core reviewer")
│   ├── 02-motor-ia.md            # coração: mensagem bruta → anúncio estruturado (JSON)
│   ├── 03-backend-supabase.md    # schema, RLS, auth, serviços, endpoints
│   ├── 04-frontend-react.md      # Vitrine, Detalhe, Login, Publicar
│   ├── 05-design-ui.md           # tokens CSS, marca ISAC, mobile-first, acessibilidade
│   ├── 06-pagamentos-comercio.md # Nível 2 — Pix sandbox + fatia pro ISAC
│   ├── 07-painel-isac.md         # Nível 2 — barra rumo a R$ 2.000/mês
│   └── 08-qa-testes-debug.md     # testes, caça-bug, checklist de apresentação
└── skills/                 # habilidades transversais (valem em qualquer frente)
    ├── seguranca-por-design/     # validação, RLS, erro/log seguros, IA sob controle
    ├── revisao-de-codigo/        # checklist de PR antes de mergear
    ├── otimizacao-performance/   # React, queries Supabase, custo/latência da IA
    ├── convencoes-do-projeto/    # nomes, pastas, CSS-vars, mobile-first, entrega
    ├── prompt-ops/               # versionar e avaliar os prompts do motor de IA
    └── git-fluxo/                # branches, commits, PR, múltiplas contas GitHub
```

## Agente x Skill (a diferença)

- **Agente** = *quem* faz uma frente. Um papel com objetivo, contexto próprio e fronteiras.
  Você "chama" um agente quando vai trabalhar naquela parte.
- **Skill** = *como* fazer certo, atravessando as frentes. É checklist/procedimento que vários
  agentes aplicam (segurança, performance, convenções…).

Cada agente lista, no fim, **quais skills ele aplica**. Assim a regra de segurança vale igual
no back, no motor de IA e no pagamento.

## Como usar

### Opção A — plugar no Claude Code / editor com IA
Os arquivos já vêm no formato certo:
- `agentes/*.md` → cole em `.claude/agents/` do repositório (têm frontmatter `name`/`description`/`tools`).
- `skills/*/SKILL.md` → cole em `.claude/skills/` (têm frontmatter `name`/`description`).

Aí é só chamar pelo nome ("usa o agente motor-ia pra…") ou deixar a skill disparar sozinha
pela descrição.

### Opção B — colar em qualquer chat de IA (Claude, Cursor, etc.)
Cada agente é autônomo. Para trabalhar numa frente, comece a conversa colando **dois** arquivos:
1. `ARQUITETURA.md` (o contexto global), e
2. o agente daquela frente (ex.: `02-motor-ia.md`).

Isso dá à IA exatamente o contexto daquela parte, sem poluir com o resto — que é o objetivo
do teu prompt de arquiteto.

### Onde colocar a pasta no repositório
Sugestão: `isac-conecta/docs/dev-kit/` (fica versionado e o grupo inteiro acha) **ou**
`isac-conecta/.claude/` se forem usar o Claude Code de verdade. Escolha uma e padronize.

## Ordem sugerida (casa com as ondas do projeto)
1. **Onda 1 (destrava tudo):** `03-backend-supabase` (banco) + `05-design-ui` (tokens/Figma).
2. **Onda 2:** `02-motor-ia` + `04-frontend-react` (Publicar e Vitrine primeiro) + integração.
3. **Onda 3 (bônus, atrás de feature flag):** `06-pagamentos-comercio` + `07-painel-isac`.
4. **Sempre por cima:** `01-arquiteto-revisor` e `08-qa-testes-debug` cuidando da coesão e do
   "funciona de verdade" pra apresentação.

## Como isso conecta tudo
`ARQUITETURA.md` fixa as camadas, as fronteiras e o contrato central (`AnuncioEstruturado`).
Cada agente trabalha dentro dessas fronteiras e aplica as skills transversais. Resultado:
controle total sobre os fluxos, estrutura clara em todos os níveis, e evolução do Nível 1 para
os Níveis 2 e 3 **sem reescrever o core**.

## Próximos passos
- Escolher o lugar da pasta no repo e commitar (`docs: adiciona dev kit de agentes e skills`).
- Preencher `backend/ia/prompts/` com o primeiro prompt real e iniciar o `prompt-ops`.
- Rodar a Onda 1 usando os agentes 03 e 05.
