---
name: seguranca-por-design
description: Segurança por design do ISAC Conecta — validação de entrada, autorização (RLS), tratamento central de erro, logging seguro e controle do motor de IA. Aplique SEMPRE que criar ou revisar rota, endpoint, formulário, tabela, política RLS, autenticação, webhook de pagamento ou chamada ao LLM. Não é opcional: toda rota e toda execução passa por aqui.
---

# Segurança por design

Segurança não é uma etapa final — é condição de cada rota e cada tabela desde o primeiro
commit. Trate esta skill como checklist obrigatório.

## 1. Validação de entrada
- Valide **toda** entrada de rota com schema (zod / JSON Schema) **antes** de tocar regra ou
  banco. Rejeite o que não bate no formato.
- Nunca confie em validação só do front — o front valida por UX, o back valida por segurança.
- Sanitize texto livre (a mensagem colada do WhatsApp) antes de mandar pra IA ou salvar.

## 2. Autorização (RLS é a fonte da verdade)
- **Toda** tabela com `enable row level security` e políticas explícitas. Sem RLS = tabela
  aberta = falha grave.
- A regra "só o dono edita" mora no banco (`auth.uid() = autor_id`), não na tela.
- Rota nunca decide autorização confiando num campo que o cliente mandou.

## 3. Erro centralizado
- Um handler único de erro. O usuário vê mensagem amigável; o log guarda o detalhe.
- **Nunca** devolva stack trace, SQL ou nome interno pro cliente.
- Falha da IA/pagamento não trava o app: degrada (anúncio fica `pendente`, assinatura fica
  `pendente`), não derruba.

## 4. Logging seguro
- **Nunca** logue: telefone completo, dados pessoais, chave de API, token, corpo de webhook cru.
- Chaves e segredos só em variável de ambiente (`.env` fora do git). Confira o `.gitignore`.
- Log serve para depurar, não para vazar. Mascare o que for PII.

## 5. Motor de IA sob controle
- Timeout em toda chamada ao LLM; retry com espera progressiva; após N tentativas → revisão.
- Rate limit para não estourar custo nem virar porta de abuso.
- Valide o JSON de volta contra o schema antes de salvar (resposta inválida = erro tratado).

## 6. Pagamento (Nível 2)
- Só o webhook validado do provedor confirma pagamento — nunca o front.
- Idempotência: mesmo evento não ativa/repassa duas vezes.

## Red flags para barrar num review
`select *` · tabela sem RLS · chave no código · rota sem validação · erro devolvendo stack ·
telefone/token em log · IA sem timeout · pagamento confirmado pelo cliente.
