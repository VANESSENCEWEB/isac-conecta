---
name: prompt-ops
description: Prompt Ops do ISAC Conecta — repositório, versionamento e avaliação dos prompts do motor de IA. Aplique SEMPRE que criar, ajustar ou testar um prompt do LLM (o que classifica/extrai anúncios), e quando montar o "Relato do processo e engenharia de prompt" que o projeto precisa documentar. Todo prompt do produto passa por aqui — nada de prompt solto no código.
---

# Prompt Ops

O motor de IA é o diferencial do projeto, e o instrutor avalia o **relato do processo e a
engenharia de prompt**. Trate prompt como código: versionado, documentado, testado.

## Onde vive
`backend/ia/prompts/` — um arquivo por prompt, versionado no git. O código carrega o prompt
desse arquivo; **nunca** string de prompt embutida no meio da lógica.

## Ficha de cada prompt (registre isto)
```md
## classificar-extrair-anuncio  (v3)
- Objetivo: transformar mensagem informal em AnuncioEstruturado (JSON).
- Contexto: grupo de bairro no Brasil, texto de voz-para-texto, gírias, sem pontuação.
- Saída esperada: JSON { titulo, categoria, preco, contato, descricao, confianca }.
- Problemas encontrados: v1 inventava preço; v2 confundia recado com anúncio;
  v3 adicionou "não invente dados" + exemplos negativos.
- Data / autor da mudança.
```

## Boas práticas de escrita do prompt
- Peça **só JSON**, sem markdown nem preâmbulo.
- Dê o enum fechado de categorias no próprio prompt.
- Inclua **exemplos negativos** ("bom dia", corrente) → confiança baixa, categoria `outro`.
- "Não invente dados que não estão na mensagem" — regra explícita contra alucinação.
- Formato de saída antes dos exemplos; exemplos curtos e representativos.

## Avaliação (mini-bateria)
Monte um conjunto fixo de ~15 mensagens reais/realistas com o resultado esperado. A cada
mudança de prompt, rode contra esse conjunto e compare:
- acertou categoria? extraiu preço/contato certo? deu confiança coerente?
- não é anúncio → confiança caiu?

Guarde o placar por versão. Assim você prova (e documenta) que o prompt **melhorou**, não só
"parece melhor".

## Ligação com outras partes
- Custo/latência de cada versão casa com `otimizacao-performance` (tokens, tempo).
- A validação de schema que barra JSON ruim é do agente `motor-ia` + `seguranca-por-design`.

## Entregável para a nota
Este repositório de prompts + a mini-bateria + o relato de evolução (v1→vN) É o material do
"Relato do processo e engenharia de prompt". Mantenha-o vivo desde o primeiro prompt.
