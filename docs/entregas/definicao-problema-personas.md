# ISAC Conecta — Definição do Problema, Personas e Validação

**Projeto:** ISAC Conecta — plataforma que organiza a economia do bairro com IA
**Instituição parceira:** ISAC — Instituto Social e Ambiental do Cabo (Enseada dos Corais, Cabo de Santo Agostinho/PE)
**Contexto:** Projeto Integrador — Residência em Software e IA (GrowUp / Porto Digital)
**Equipe:** Vanessa Rafaella (coordenação) e equipe — _[preencher nomes]_
**Versão:** 1.1 · **Data:** 19/09/2026 · **Status:** em desenvolvimento (Fase 1)

---

## 1. Descrição do problema, solução e oportunidade de IA

### 1.1 Problema _(224 caracteres)_
Nos grupos de WhatsApp do bairro, os anúncios de produtos, serviços e vagas se perdem no fluxo de mensagens: sem busca, filtro ou organização, boas ofertas somem em minutos. Quem procura não encontra; quem oferece não vende.

### 1.2 Solução
Uma plataforma web onde o morador publica o anúncio **do mesmo jeito que já escreve no WhatsApp** — colando a mensagem informal. Uma IA lê o texto, identifica que é um anúncio e o transforma em um card organizado (categoria, preço, contato, local), que entra numa **vitrine pesquisável com busca e filtro**. Do lado do ISAC, o modelo gera **receita recorrente** (comércios pagam por destaque), sustentando a instituição.

### 1.3 Onde a IA gera valor
A IA é o coração do produto e atua em três frentes, explicitamente:

- **Automação** — elimina o trabalho manual de catalogar. A extração e estruturação do anúncio (do texto solto para campos organizados) acontece sozinha, em segundos.
- **Predição / classificação** — o modelo decide **se a mensagem é um anúncio** e **em qual categoria** se encaixa, atribuindo um **grau de confiança**; abaixo do limiar, o item vai para revisão em vez de ir direto ao ar.
- **Geração de conteúdo** — normaliza e limpa o texto informal, gerando **título e descrição padronizados** a partir da mensagem original (evolução futura: sugestões de melhoria do anúncio).

---

## 2. Personas, cenários de uso e casos de borda

### 2.1 Personas

**Dona Maria — a vendedora do bairro (52 anos)**
Faz cestas orgânicas e doces por encomenda. Anuncia nos grupos, mas a mensagem some no meio de conversas. **Dor:** "posto e ninguém vê; quando veem, já rolou muita coisa por cima."

**Rafael — o morador que procura (28 anos)**
Busca aluguel de temporada, serviços e desapegos. **Dor:** "tenho que rolar 200 mensagens pra achar uma coisa, e quando acho o contato já vendeu."

**Bia — o comércio local (pousada / aluguel)**
Quer alcance e previsibilidade de clientes. **Dor:** "dependo de indicação e sorte; queria aparecer pra quem está procurando de verdade."

**ISAC — a instituição (stakeholder)**
Precisa de uma fonte de receita recorrente para sustentar seus programas. **Dor:** "faltam recursos previsíveis para manter as ações no bairro."

### 2.2 Cenários de uso (fluxo principal)

- **Publicar:** Dona Maria cola "vendo cesta orgânica 45 zap 9 9999" → a IA monta o card (Produto · R$ 45 · contato) → ela confirma → o anúncio entra na vitrine.
- **Buscar:** Rafael abre a vitrine, filtra por "Imóveis", busca "frente-mar" → encontra o anúncio → toca em contato → abre o WhatsApp do anunciante.

### 2.3 Casos de borda (edge cases de IA)

- Mensagem que **não é anúncio** ("bom dia", corrente, recado) → confiança baixa, categoria "outro", **não publica**.
- Anúncio **incompleto** (sem preço ou sem contato) → campos ficam nulos ("a combinar"), sistema pede complemento.
- **Áudio transcrito** com gírias, erros de digitação ou pontuação ausente.
- **Vários itens** numa mensagem só.
- **Preço em formato atípico** ("250 conto", "2 e meio", "a partir de").
- Conteúdo **impróprio ou golpe** → vai para moderação/pendente, não entra direto na vitrine.

### 2.4 Cenários de falha e casos críticos de erro

- **IA indisponível / timeout** → o anúncio fica "pendente", o app **não trava**, e há nova tentativa (retry progressivo).
- **Resposta inválida do modelo** (JSON quebrado) → a validação de schema **barra antes de salvar**; nada corrompido entra no banco.
- **Alucinação** (inventar preço/contato) → regra explícita "não inventar dados" + revisão pelos itens de baixa confiança.
- **Estouro de custo/limite da API** → cache por mensagem repetida, processamento em lote e limite de uso.
- **Vazamento de dado sensível** (telefone em log) → logging seguro, sem PII, chaves só em variáveis de ambiente.

---

## 3. Confiança e verificação

Confiança é o requisito crítico do produto: sem ela, ninguém publica nem compra. A credibilidade é construída em camadas.

- **Autoria — quem publica é a pessoa logada.** O sistema **não** pega texto de qualquer um no grupo: o próprio morador entra na plataforma (cadastro/login) e cola a mensagem dele. Todo anúncio fica amarrado a uma conta real (`autor_id`). **Nada anônimo entra na vitrine.**
- **Verificação de telefone → selo "Verificado".** Como o contato é via WhatsApp, a plataforma envia um **código para o número** e a pessoa confirma. Só então o número recebe o selo — que passa a significar algo real: aquele contato existe e é do anunciante. _(MVP: confirmação simples; verificação por código/OTP completa se houver tempo.)_
- **Limiar de confiança + moderação.** Anúncio ambíguo, suspeito ou que a IA não entendeu bem entra como **"pendente"** e não vai direto ao ar.
- **Contato direto com o anunciante verificado.** O botão de contato leva ao WhatsApp de quem realmente publicou — a conversa acontece com o dono do anúncio.
- **Selo de comércio parceiro (chancela do ISAC).** O Instituto pode validar comércios locais, emprestando a credibilidade institucional a quem é parceiro.
- **Reputação e avaliações (Nível 3, futuro).** Histórico e notas de quem já negociou.

**Sobre a leitura automática do grupo:** fica para o **Nível 3**. E, mesmo lá, a IA apenas cria um **rascunho pendente** — que só vai ao ar quando o dono **reivindica e confirma** ("esse anúncio é meu"). O sistema nunca publica em nome de alguém sem essa confirmação.

---

## 4. Entrevistas e validação de hipóteses

### 4.1 Hipóteses a validar
- **H1 — Dor real:** moradores perdem oportunidades por causa da desorganização dos grupos.
- **H2 — Adoção:** as pessoas topariam publicar "do jeito que já fazem" se isso virasse algo organizado e pesquisável.
- **H3 — Sustentabilidade:** comércios locais pagariam por destaque/alcance.

### 4.2 Roteiro de entrevista (foco em pontos de dor)
1. Como você anuncia ou procura coisas no bairro hoje?
2. Já perdeu uma venda ou uma oportunidade porque o anúncio "se perdeu" no grupo?
3. O que é mais chato nesse processo hoje?
4. Se pudesse colar a mesma mensagem e ela virasse um anúncio organizado e pesquisável, usaria? Por quê?
5. (Comércio) Pagaria por destaque para aparecer a quem está procurando? Quanto faria sentido?

### 4.3 Relatório — entrevista com humanos
> **A preencher após as entrevistas.** Meta: pelo menos **1 entrevista com humano** para validação do problema.
>
> - Entrevistado(a): _[nome / perfil]_
> - Data: _[data]_
> - Principais dores levantadas: _[preencher]_
> - Hipóteses confirmadas/refutadas: _[preencher]_
> - Aprendizados e ajustes no produto: _[preencher]_

### 4.4 Relatório — entrevista com agentes inteligentes
> **A preencher.** Simulação de entrevista com uma IA assumindo o papel de uma persona (ex.: "Dona Maria"), para antecipar pontos de dor e testar o roteiro antes de ir a campo.
>
> - Persona simulada: _[preencher]_
> - Principais dores levantadas: _[preencher]_
> - O que essa simulação sugeriu ajustar no roteiro/produto: _[preencher]_

---

## 5. Status atual do projeto (para acompanhamento)

- ✅ **Design System v2.0** "Praia, mata e vizinhança" (Inter, base 4px, WCAG AA) — proposta pronta.
- ✅ **Repositório organizado** com documentação, arquitetura, agentes e skills de desenvolvimento.
- 🔵 **Telas** em construção — Home e Classificados (vitrine) já prototipadas.
- 🔵 **Banco de dados** (Supabase) — modelagem iniciando (perfis, anúncios, categorias + RLS).
- ⬜ **Motor de IA** (classificação/extração) — próxima etapa.
- ⬜ **Entrevistas** de validação — a realizar.

**Próximos passos:** concluir as telas do Nível 1, subir o schema do banco, escrever o primeiro prompt do motor de IA e realizar a primeira entrevista de validação.
