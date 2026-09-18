# Arquitetura Global — ISAC Conecta

> Este é o **contexto compartilhado**. Todo agente da pasta `agentes/` começa lendo este
> arquivo. Ele fixa a arquitetura, as fronteiras entre módulos e os pontos de segurança.
> Ninguém reescreve o "core" — cada agente trabalha dentro das fronteiras aqui definidas.

## 1. O que o sistema é

Plataforma web que usa IA para transformar o caos dos grupos de WhatsApp na **economia
organizada do bairro**, e converte isso em receita recorrente que sustenta o ISAC.

Fluxo-coração:

```
mensagem bruta                IA (LLM)                card estruturado        vitrine
"vendo fogão 4 bocas    ──►  classifica +      ──►   {categoria, preço,  ──►  pesquisável
 250 zap 9 9999"             extrai                    contato, título}         + filtro
```

## 2. Princípios inegociáveis

1. **Arquitetura primeiro.** Nada de código antes das fronteiras estarem claras.
2. **Modularização real.** Domínio, regra de negócio e interface ficam separados de verdade.
3. **Segurança por design.** Toda rota valida entrada, checa autorização e trata erro de
   forma centralizada. Ver `skills/seguranca-por-design`.
4. **Baixo acoplamento, alta coesão.** Nenhuma parte fala com a IA direto, só o módulo `ia/`.
5. **Evolução incremental.** MVP hoje; níveis 2 e 3 entram sem reescrever o essencial.

## 3. Camadas

| Camada | Responsabilidade | Onde vive |
|---|---|---|
| **Apresentação** | Telas, componentes, responsividade | `frontend/` (React) |
| **Aplicação** | Orquestra casos de uso, valida entrada, autoriza | `backend/rotas` + `backend/servicos` |
| **Domínio** | Entidades e regras (Anúncio, Perfil, Comércio) | `backend/modelos` |
| **Infraestrutura** | Banco, auth, IA, pagamento | Supabase + `backend/ia` + provedor Pix |

A IA é **infraestrutura**, não domínio. Trocar de modelo LLM não pode encostar no resto.

## 4. Estrutura de pastas

```
isac-conecta/
├── frontend/
│   ├── src/
│   │   ├── paginas/       # Vitrine, Detalhe, Login, Publicar, AreaComercio, PainelISAC
│   │   ├── componentes/   # Card, Busca, Filtro, Selo, BarraImpacto (reutilizáveis)
│   │   ├── servicos/      # cliente supabase, chamadas à API (nada de fetch solto na tela)
│   │   ├── estilos/       # tokens.css (variáveis) + globais
│   │   └── hooks/         # useAnuncios, useAuth, etc.
├── backend/
│   ├── rotas/            # endpoints / edge functions — ponto de segurança
│   ├── servicos/         # regras de negócio (publicar anúncio, promover comércio)
│   ├── ia/              # ISOLA o LLM: prompts, parser, validação de schema, retry
│   └── modelos/         # entidades + schema do banco (fonte da verdade)
├── banco/               # migrações SQL + políticas RLS
└── docs/                # este dev kit vive aqui (ou em .claude/, ver README)
```

## 5. Contratos entre módulos (interfaces)

O card estruturado é o **contrato central**. Todo módulo fala nesse formato:

```jsonc
// AnuncioEstruturado — saída do motor de IA e linha da tabela `anuncios`
{
  "id": "uuid",
  "titulo": "Fogão 4 bocas",
  "categoria": "eletrodomestico",     // enum fechado, ver modelos
  "preco": 250.00,                     // number | null (null = "a combinar")
  "contato": "(81) 9 9999-9999",       // normalizado
  "descricao": "texto original limpo",
  "status": "ativo",                   // ativo | pendente | expirado
  "confianca": 0.92,                   // 0..1 vindo da IA (abaixo do limiar → revisão)
  "autor_id": "uuid",
  "criado_em": "timestamptz"
}
```

- **Front → Back:** só chama `frontend/src/servicos`. Nunca monta SQL nem chama a IA.
- **Back → IA:** só o `backend/ia` conhece o LLM. Devolve `AnuncioEstruturado` validado ou erro.
- **Back → Banco:** via `modelos`. RLS ligado em toda tabela (ver segurança).

## 6. Pontos de segurança (integrados desde o início)

- **Validação de entrada** em toda rota (schema/zod) antes de tocar em regra ou banco.
- **Autorização**: RLS no Supabase é a fonte da verdade; a rota nunca confia no front.
- **Erro centralizado**: um handler único; nunca vaza stack/segredo pro usuário.
- **Logging seguro**: sem PII, sem telefone completo em log, sem chave de API.
- **IA sob controle de custo/abuso**: timeout, retry progressivo, rate limit, cache, batch.

## 7. Escalabilidade e evolução (pontos de extensão)

- **Inversão de dependência no `ia/`**: interface `MotorDeAnuncios` → hoje LLM, amanhã outro.
- **Feature flags / config externa** para ligar Nível 2 (área comercial, painel) sem deploy.
- **Categorias como dado** (tabela), não hardcode — o bairro muda, o enum não trava.
- **Fila/assíncrono** no processamento de mensagens para aguentar lote da demonstração.

## 8. Escopo por nível (o que cada agente pode assumir como pronto)

- **Nível 1 (MVP, entrega 02/out):** motor de IA, vitrine com busca/filtro, cadastro simples.
  Páginas: Início/Vitrine, Detalhe, Login/Cadastro, Publicar.
- **Nível 2 (se der tempo):** Área do comércio (perfil pago/destaque), Painel do ISAC
  (barra rumo a R$ 2.000), selo de confiança.
- **Nível 3 (só documentado):** leitura automática do WhatsApp, LocalMatch, reputação,
  Pix recorrente, app mobile. **Não implementar** — só deixar pontos de extensão.

## 9. Stack fixada

React (web responsivo) · Supabase (PostgreSQL + Auth + RLS) · API de LLM para o motor ·
provedor de pagamento com Pix + sandbox. Custo: tudo gratuito no MVP; único custo variável
é a API de IA, controlada por limiar, cache e processamento em lote.
