<div align="center">

# 🌱 ISAC Conecta

### A economia do bairro, organizada por Inteligência Artificial

Plataforma web que usa IA para transformar a bagunça dos grupos de WhatsApp
na **economia organizada do bairro** — e essa organização vira **renda para o ISAC**.

<br>

![Status](https://img.shields.io/badge/status-em%20desenvolvimento-yellow)
![Projeto](https://img.shields.io/badge/projeto-GrowUp%20%2F%20Porto%20Digital-blue)
![HTML](https://img.shields.io/badge/HTML-98.8%25-orange)
![CSS](https://img.shields.io/badge/CSS-1.2%25-563d7c)
![Licença](https://img.shields.io/badge/uso-acad%C3%AAmico-lightgrey)

[🌐 Ver site](https://vanessenceweb.github.io/isac-conecta/) ·
[📄 Documentos](#-documentos) ·
[🗺️ Fases](#️-fases-do-projeto) ·
[👥 Equipe](#-divisão-de-tarefas) ·
[🤝 Como colaborar](#-como-colaborar)

</div>

---

## 📑 Sumário

- [Sobre o projeto](#-sobre-o-projeto)
- [O problema](#-o-problema)
- [A solução](#-a-solução)
- [Como funciona](#️-como-funciona)
- [Modelo de negócio](#-modelo-de-negócio)
- [Fases do projeto](#️-fases-do-projeto)
- [Escopo do MVP](#-escopo-do-mvp)
- [Tecnologias](#-tecnologias)
- [Divisão de tarefas](#-divisão-de-tarefas)
- [Documentos](#-documentos)
- [Como colaborar](#-como-colaborar)
- [Sobre o ISAC](#-sobre-o-isac)
- [Equipe](#-equipe)

---

## 🎯 Sobre o projeto

**ISAC Conecta** é o projeto integrador da **Residência em Software & IA** (GrowUp / Porto Digital), desenvolvido para o desafio do **Instituto Social e Ambiental do Cabo (ISAC)**, no Cabo de Santo Agostinho (PE).

Hoje, tudo que se vende, aluga ou oferece no bairro some no meio das mensagens dos grupos de WhatsApp. Nosso sistema usa **inteligência artificial** para ler esses anúncios bagunçados e transformá-los em uma **vitrine limpa e pesquisável**, onde qualquer pessoa acha o que procura em segundos.

E tem um **propósito social**: a plataforma cobra dos comércios que querem aparecer e repassa parte para o ISAC, ajudando o instituto a ter uma renda mensal. Ou seja: **organiza o bairro e sustenta quem cuida dele.**

---

## 🔴 O problema

A economia da comunidade vive dentro do WhatsApp — grupos com centenas de moradores que passam de **2 mil mensagens por dia**.

| Dor | Impacto |
|-----|---------|
| Tudo misturado (produto, serviço, vaga, imóvel, evento) | Sem categoria, sem busca, sem histórico |
| O anúncio some em minutos | O pequeno empreendedor perde alcance |
| ISAC sem receita fixa | A instituição vive de doação e rifa |

---

## 🟢 A solução

Uma plataforma inteligente que organiza as oportunidades locais:

- 📥 A pessoa manda a mensagem **do jeito que já manda**
- 🤖 A IA **classifica e extrai** categoria, preço, telefone e localização
- 🗂️ Vira um **anúncio estruturado** numa vitrine com busca e filtro
- 🛡️ Cada anúncio ganha um **selo de confiança**

---

## ⚙️ Como funciona

```
┌──────────────────────────┐      ┌──────────┐      ┌──────────────────────────┐
│   Mensagem bruta         │      │          │      │   Card estruturado       │
│ "vendo fogão 4 bocas     │ ───▶ │    IA    │ ───▶ │  Categoria: Produtos     │
│  250 zap 9999"           │      │          │      │  Preço: R$ 250           │
│                          │      │          │      │  Contato: (81) 9 9999    │
└──────────────────────────┘      └──────────┘      └──────────────────────────┘
                                                              │
                                                              ▼
                                                     🔎 Vitrine pesquisável
```

1. Uma mensagem de anúncio entra no sistema
2. A IA lê e entende — identifica que é um anúncio e separa as informações
3. Vira um card organizado — com categoria, preço e contato certinhos
4. Aparece na vitrine — pesquisável por qualquer morador

---

## 💰 Modelo de negócio

Dois lados que se sustentam:

| Lado | Para quem | O que oferece |
|------|-----------|---------------|
| 🆓 **Gratuito** | Toda a comunidade | Consultar e divulgar oportunidades |
| ⭐ **Premium** | Empresas e profissionais | Destaque e maior visibilidade |

> 🎯 **Meta:** a receita recorrente gera cerca de **R$ 2.000/mês para o ISAC** — o primeiro dinheiro previsível da instituição.

---

## 🗺️ Fases do projeto

O caminho completo até o projeto ficar pronto para apresentação:

| Fase | Etapa | O que inclui | Status |
|:----:|-------|--------------|:------:|
| **1** | 🏗️ Fundação | Figma (design das telas) + Banco de dados (Supabase) | 🔄 Em andamento |
| **2** | 🚀 Construção | Motor de IA + Front-end das telas + Integração | ⏳ Aguardando |
| **3** | ✨ Bônus | Área do comércio + Painel do ISAC + Selo de confiança | ⏳ Aguardando |
| **4** | 🎤 Fechamento | Documentação + Business Model Canvas + Apresentação | ⏳ Aguardando |

> **Fase 1 destrava tudo:** enquanto o Figma e o banco não andam, o front-end não começa. O foco inicial é aqui.

---

## 📋 Escopo do MVP

Dividido em três níveis para o grupo não construir no escuro:

### ✅ Nível 1 — Essencial (tem que funcionar)
- **Motor de IA** — lê a mensagem e transforma em anúncio estruturado
- **Vitrine de anúncios** — lista os cards com busca e filtro por categoria
- **Cadastro simples** — morador/comerciante cria conta e publica

### 🟡 Nível 2 — Se der tempo (bônus que valoriza)
- **Área do comércio** — perfil pago e destaque de anúncio
- **Painel do ISAC** — barra de arrecadação rumo aos R$ 2.000/mês
- **Selo de confiança** — marca anunciante verificado (contra golpe)

### ⏳ Nível 3 — Próxima fase (só documentado)
- Leitura automática do WhatsApp
- LocalMatch — recomendação inteligente de oportunidades
- Reputação e badges, Pós-Conexão, Pix recorrente, app mobile

### 🖥️ Páginas do site

| Página | O que tem | Nível |
|--------|-----------|:-----:|
| Início / Vitrine | Lista de anúncios, busca e filtro por categoria | Essencial |
| Detalhe do anúncio | Card completo: foto, preço, contato, categoria | Essencial |
| Login / Cadastro | Criar conta e entrar (morador ou comércio) | Essencial |
| Publicar anúncio | Campo para colar a mensagem; a IA estrutura | Essencial |
| Área do comércio | Perfil pago e botão de destaque | Se der tempo |
| Painel do ISAC | Arrecadação do mês e barra da meta | Se der tempo |

> 💡 **Ordem de construção:** começar por **Publicar + Vitrine**, porque são elas que mostram a IA funcionando. Desenhar no **Figma antes de programar** economiza retrabalho.

---

## 🛠️ Tecnologias

| Camada | Tecnologia |
|--------|-----------|
| Front-end | React · Web responsivo |
| Back-end / Banco | Supabase (PostgreSQL + Auth) |
| Motor de IA | API de LLM |
| Pagamentos | Provedor com Pix + sandbox |
| Design | Figma |
| Versionamento | Git + GitHub |

---

## 👥 Divisão de tarefas

Organização por **frentes**, em ondas. Os nomes servem para orientar — dá para trocar de frente, ajudar o colega ou pegar mais de uma coisa. **Quem terminar, ajuda quem tiver dificuldade.**

### 🌊 Onda 1 — Começa agora (destrava o resto)

| Frente | Responsável | Descrição |
|--------|-------------|-----------|
| 🎨 Design / Figma | `@____` | Desenhar as telas: Vitrine, Detalhe, Publicar, Login |
| 🗄️ Banco de dados | `@____` | Modelar tabelas: usuários, anúncios, categorias |

### 🌊 Onda 2 — Entra quando o Figma e o banco estiverem prontos

| Frente | Responsável | Descrição |
|--------|-------------|-----------|
| 🤖 Motor de IA | `@____` | Prompt que transforma mensagem bruta em anúncio estruturado |
| 💻 Front — Vitrine + Detalhe | `@____` | Tela principal com lista, busca e filtro |
| 📝 Front — Publicar + Login | `@____` | Tela de colar a mensagem + criar conta/entrar |
| 🔗 Integração | `@____` | Junta front + IA + banco |

### 🌊 Onda 3 — Bônus e fechamento

| Frente | Responsável | Descrição |
|--------|-------------|-----------|
| ✨ Área do comércio + Painel ISAC | `@____` | Perfil pago, destaque e barra de arrecadação |
| 📋 Documentação + Apresentação | `@VANESSENCEWEB` | Escopo, Business Model Canvas e apresentação final |

---

## 📂 Documentos

Todo o material do grupo está reunido neste repositório:

| Documento | Descrição |
|-----------|-----------|
| 📄 `desafio-projeto.pdf` | Enunciado oficial do desafio |
| 📄 `ISAC_Conecta_Escopo.pdf` | Escopo do projeto (funções, páginas, níveis) |
| 📄 `divisao-tarefas-equipe.pdf` | Divisão de tarefas da equipe |
| 📄 `ISAC_Conecta_Divisao_Tarefas_v2.pdf` | Divisão de tarefas (versão atualizada) |
| 📄 `questionario-respondido-pela-isac.pdf` | Questionário respondido pelo instituto |

---

## 🤝 Como colaborar

Trabalhamos de forma colaborativa no GitHub. Para contribuir:

1. **Aceite o convite** de collaborator do repositório
2. **Crie uma branch** a partir da `main`:
   ```bash
   git checkout main
   git pull origin main
   git checkout -b feat/seu-nome
   ```
3. **Faça seus commits** na sua branch:
   ```bash
   git add .
   git commit -m "feat: descrição da mudança"
   git push origin feat/seu-nome
   ```
4. **Abra um Pull Request** para a `main`

> ⚠️ **Não commite direto na `main`.** Todo código entra por Pull Request, para o grupo revisar junto.

---

## 🌍 Sobre o ISAC

O **Instituto Social e Ambiental do Cabo (ISAC)** é uma organização sem fins lucrativos do Cabo de Santo Agostinho (PE). Atua em:

- 🌳 Educação ambiental e reflorestamento da Mata Atlântica
- 🤝 Inclusão social
- 📢 Defesa de políticas públicas

Associação civil sem fins econômicos, fundada em julho de 2023, mantida por diretores e voluntários. Hoje não possui receita recorrente — depende de doações e rifas. O ISAC Conecta nasce para ajudar a mudar isso.

🔗 **Site do instituto:** [isac-instituto.org.br](https://isac-instituto.org.br)

---

## 👩‍💻 Equipe

Projeto desenvolvido pelo grupo da Residência em Software & IA — GrowUp / Porto Digital.

**Coordenação e desenvolvimento:** [@VANESSENCEWEB](https://github.com/VANESSENCEWEB) (Vanessa Lima)

<div align="center">

---

<sub>© 2026 · Projeto acadêmico ISAC Conecta · GrowUp / Porto Digital</sub>

</div>
