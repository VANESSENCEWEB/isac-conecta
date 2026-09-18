---
name: revisao-de-codigo
description: Checklist de revisão de código do ISAC Conecta antes de mergear. Aplique SEMPRE que for revisar um PR, juntar o trabalho de duas pessoas do grupo, ou antes de aprovar qualquer mudança que vá para a branch principal. Use também quando alguém pedir "revisa isso pra mim" ou "tá bom pra subir?".
---

# Revisão de código

O grupo tem 8 pessoas mexendo em paralelo. A revisão é o que impede o Frankenstein. Passe todo
PR por este checklist — objetivo, não perfeccionista: bloqueie o que quebra, comente o resto.

## Bloqueia o merge (P1)
- [ ] **Fronteiras respeitadas:** tela não chama IA nem SQL direto; só `motor-ia` fala com o LLM.
- [ ] **Segurança:** passa na skill `seguranca-por-design` (RLS, validação, sem chave no código,
      erro não vaza).
- [ ] **Contrato:** usa `AnuncioEstruturado` como combinado; não inventou formato paralelo.
- [ ] **Funciona:** rodou? tem teste do caminho principal e dos estados de erro?
- [ ] **Sem segredo commitado** e `.env` no `.gitignore`.

## Comenta, não bloqueia (P2)
- [ ] Nomes claros e em pt (segue `convencoes-do-projeto`).
- [ ] Arquivo no lugar certo da estrutura da arquitetura.
- [ ] Sem código morto, `console.log` esquecido, TODO sem dono.
- [ ] Componente/serviço com uma responsabilidade só.
- [ ] Estados de tela (carregando/vazio/erro) tratados.

## Como comentar
Seja específico e gentil — é o trabalho de um colega sob prazo apertado.
```
[arquivo:linha] <o quê> — <por quê importa> — <sugestão concreta>
```
Elogie o que ficou bom também; revisão não é só apontar defeito.

## Tamanho do PR
PR gigante ninguém revisa direito. Prefira PRs pequenos por frente/onda. Se vier enorme,
peça pra fatiar antes de revisar a fundo.

## Antes de aprovar
Pergunte a si mesmo: "isso trava o Nível 2/3?" Se travar sem necessidade, peça um ponto de
extensão em vez de solução fechada.
