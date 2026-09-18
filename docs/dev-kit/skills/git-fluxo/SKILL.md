---
name: git-fluxo
description: Fluxo de git do ISAC Conecta para um grupo de 8 pessoas trabalhando em paralelo em ondas. Aplique quando alguém for criar branch, commitar, abrir PR, resolver conflito, ou quando precisar organizar o repositório para o grupo. Use também para lembrar como separar as contas GitHub (estudo vs. pessoais) na hora de commitar.
---

# Fluxo de git (grupo de 8)

Com 8 pessoas e prazo até 02/out, o repositório precisa de disciplina simples — não um
fluxo enterprise que ninguém segue.

## Branches (por onda/frente da arquitetura)
- `main` — sempre funcional; é o que vai pra apresentação. Ninguém commita direto.
- `feat/motor-ia`, `feat/vitrine`, `feat/banco`, `feat/design`… uma branch por frente.
- Branch curta e viva: abre, faz, PR, mergeia, apaga. Nada de branch de 3 semanas.

## Commits (conventional commits em pt)
```
feat: adiciona extração de preço no motor de IA
fix: corrige RLS que deixava editar anúncio de outro
style: aplica tokens de cor no card
docs: registra prompt v3 no prompt-ops
```
Mensagem no imperativo, específica. "ajustes", "wip", ".", "aaa" não passam.

## Pull Request
- PR pequeno, com o que mudou e como testar em 2 linhas.
- Passa pela skill `revisao-de-codigo` antes do merge.
- Pelo menos 1 revisão de outra pessoa da onda antes de entrar na `main`.

## Conflitos
- Puxe `main` na sua branch com frequência (`git pull --rebase origin main`) — conflito pequeno
  e cedo é fácil; conflito grande na véspera é desespero.
- Conflito de estrutura (dois mexeram na mesma fronteira) → chame o `arquiteto-revisor`.

## Múltiplas contas GitHub (setup da Vanessa)
Você usa contas separadas (estudo, `vanessenceweb`, `recife-flats`). Para o PI, commite com a
conta de **estudo**. Cheque antes de commitar:
```bash
git config user.email        # confere qual identidade está ativa no repo
```
Se estiver errada, ajuste **local** (só neste repo), não global:
```bash
git config user.email "seu-email-de-estudo@exemplo.com"
git config user.name  "Vanessa (estudo)"
```
Com chaves SSH por conta, garanta que o `remote` usa o host certo do seu `~/.ssh/config`.

## .gitignore (confira já no início)
`node_modules/`, `.env`, `.env.*`, build/dist, arquivos de credencial. Segredo commitado é
incidente de segurança — ver `seguranca-por-design`.

## Higiene do repo
README na raiz explicando como rodar (front, back, migrações). O dev kit vive em `docs/` ou
`.claude/` (ver README do kit). Deixe o `main` sempre clonável e rodável — é o que o avaliador
pode pedir para ver.
