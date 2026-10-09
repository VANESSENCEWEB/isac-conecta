# Telas do ISAC Conecta

Exportações das telas desenhadas no Figma, para quem vai programar o front-end consultar sem precisar abrir o arquivo.

- **Arquivo no Figma:** https://www.figma.com/design/NBL7y7pfsTsTqk5Kv6xhUc
- **Cores, tipografia e espaçamentos:** `docs/design-system/tokens.css`
- **Formato:** mobile, 390 px de largura (mobile-first). Desktop vem depois.

> O Figma é a fonte da verdade. Se uma tela mudar lá, exporte de novo e substitua o PNG aqui com o mesmo nome.

## Status das telas

| # | Tela | Arquivo | Nível | Status |
|---|------|---------|:-----:|--------|
| 01 | Vitrine (início) | `mobile/01-vitrine.png` | 1 | ✅ Pronta |
| 02 | Detalhe — anúncio importado do grupo | `mobile/02-detalhe-importado-do-grupo.png` | 1 | ✅ Pronta |
| 03 | Detalhe — comércio verificado | `mobile/03-detalhe-comercio-verificado.png` | 1 | ✅ Pronta |
| 04 | Login | `mobile/04-login.png` | 1 | 🔄 Em ajuste |
| 05 | Cadastro | `mobile/05-cadastro.png` | 1 | 🔄 Em ajuste |
| 06 | Publicar · 1 Entrada | `mobile/06-publicar-1-entrada.png` | 1 | 🔄 Em ajuste |
| 07 | Publicar · 2 Processando | `mobile/07-publicar-2-processando.png` | 1 | ✅ Pronta |
| 08 | Publicar · 3 Revisão | `mobile/08-publicar-3-revisao.png` | 1 | 🔄 Em ajuste |
| — | Publicar · versão morador | — | 1 | ⏳ A fazer |
| — | Fila de moderação (ISAC) | — | 1 | ⏳ A fazer |
| — | Confirme seu e-mail | — | 1 | ⏳ A fazer |
| — | Estados: nenhum resultado, erro da IA, carregando | — | 1 | ⏳ A fazer |
| — | Meus anúncios e Perfil | — | 1 | ⏳ A fazer |
| — | Planos do comércio | — | 2 | ⏳ A fazer |
| — | Área do comércio | — | 2 | ⏳ A fazer |
| — | Painel do ISAC | — | 2 | ⏳ A fazer |

## O que cada tela faz

**01 · Vitrine** — busca, filtro por distância e categoria, carrossel de destaques (comércios pagos), lista de anúncios com selo de verificado e aviso de anúncios repetidos agrupados.

**02 e 03 · Detalhe do anúncio** — duas variações do mesmo componente:
- *Importado do grupo:* anúncio que veio da conversa do WhatsApp; o ISAC revisou, mas o anunciante não tem conta verificada.
- *Comércio verificado:* anunciante conferido pelo ISAC, com selo "Verificado".
Ambas têm o aviso fixo "Negocie com segurança", o link "Denunciar anúncio" e o botão "Chamar no WhatsApp".

**04 e 05 · Login e Cadastro** — entrar com e-mail e senha; criar conta.

**06 a 08 · Publicar (fluxo de 3 passos)** — o coração da demo:
1. *Entrada:* colar uma mensagem ou importar a conversa do grupo (.txt).
2. *Processando:* a IA lê, separa o que é anúncio, extrai preço/categoria/contato e checa duplicados e golpes.
3. *Revisão:* cards editáveis com o texto original; duplicados agrupados e possíveis golpes desmarcados.

## Versões anteriores

`versoes-anteriores/` guarda telas substituídas, só para registro do processo. Não use como referência para o código.

## Como adicionar uma tela nova

1. No Figma, selecione o frame da tela → painel **Export** → `PNG`, `2x` → **Export**.
2. Nomeie seguindo o padrão `NN-nome-da-tela.png` (ex.: `09-fila-moderacao.png`), tudo minúsculo, sem acento e sem espaço.
3. Coloque em `mobile/` (ou `desktop/`) e atualize a tabela acima.
4. Commit: `docs(design): adiciona tela de fila de moderação`.
