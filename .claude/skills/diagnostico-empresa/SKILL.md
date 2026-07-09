---
name: diagnostico-empresa
description: >
  Gera um diagnóstico digital poderoso de uma empresa a partir do site, Instagram e Google Maps
  — raspa o que é público, pesquisa os concorrentes reais, calcula um Score de Saúde Digital,
  aponta as vulnerabilidades priorizadas por impacto, estima o dinheiro deixado na mesa e monta
  um plano de 24h + roadmap de 90 dias, tudo amarrado nos produtos e serviços do seu negócio.
  Entrega um relatório HTML no padrão da apresentação e, quando faz sentido, um protótipo de
  loja/app na marca do cliente pra demonstrar ao vivo. Use quando o usuário disser "diagnóstico",
  "/diagnostico-empresa", "avaliar empresa", "raio-x digital", "vou apresentar pra um cliente",
  "análise de concorrente", ou mandar o site/@/Maps de uma empresa pra avaliar.
---

# /diagnostico-empresa — Raio-X digital pra fechar cliente

Diagnóstico é uma arma comercial de entrada: um relatório que raspa a presença digital de um
prospect, mostra onde ele perde dinheiro, compara com os concorrentes reais e já aponta o que o
seu negócio resolve — separando o que dá pra entregar em 24h (isca) do que é projeto maior
(upsell). Não é auditoria técnica; é peça de venda honesta e concreta.

O objetivo de cada diagnóstico é chegar num **ângulo central** — uma frase que reposiciona a
conversa. Ex.: *"você tem o estoque e a audiência, falta a máquina que vende."* Procure sempre
esse ângulo: o ativo caro que o cliente já tem e não está convertendo.

> **Adapte ao seu negócio.** Esta skill mapeia cada gargalo encontrado para um produto/serviço
> **do seu negócio**. Antes de usar em produção, ajuste a seção "Passo 4 — Plano" e o mapa de
> solução para as suas ofertas reais (o que você vende). O método, o score e o design do
> relatório servem pra qualquer segmento — só o mapa de solução é seu.

## Entradas que peço ao usuário

- **Site** do prospect (obrigatório)
- **@ do Instagram** e **link/nome do Google Maps**
- **Ramo** do negócio e cidade
- **Concorrentes** que ele citar (opcional — e quase sempre incompletos; ver passo de concorrência)

## Contexto a carregar

`_memoria/empresa.md` (o que o seu negócio vende, pra montar o mapa de solução) e
`_memoria/preferencias.md` (tom de voz e o que evitar na escrita do relatório).

---

## Passo 1 — Coleta de dados (raspagem do que é público)

Se houver um agente para tarefas mecânicas de volume, delegue as buscas amplas a ele. Fontes e
como pegar:

- **Site (fácil, rico):** `WebFetch`. Extrair: tem e-commerce/carrinho/catálogo online? WhatsApp e
  CTA claro? Pixel/analytics/chat? Plataforma (WordPress, Shopify…)? Qualidade do copy e da
  conversão. É a maior parte do diagnóstico.
- **Instagram (difícil):** o IG bloqueia raspagem. Use `WebSearch` por "@handle seguidores" pra
  pegar nº de seguidores/posts. Trate o resto como análise qualitativa (perfil ativo? tem link de
  compra na bio? identidade visual?). **Nunca** dependa de raspar IG automático.
- **Google Maps:** links `share.google` costumam cair em página de erro e raspar o Maps direto é
  frágil. O caminho limpo é a **Places API** (grátis no início, precisa de key). Sem key: **peça a
  nota e o nº de avaliações ao usuário** — é rápido e a nota é um dado de ouro.
- **Meta Ad Library** (`facebook.com/ads/library`): mostra se anuncia. É pesado de JS e costuma não
  carregar via WebFetch — se falhar, **não afirme nada** sobre tráfego pago (não erre por chute);
  marque "verificar ao vivo".

Regra de honestidade: o que não conseguir confirmar vira **n/d** ou "a validar". Nunca invente
número. Estimativas de R$ são sempre rotuladas como ilustrativas.

## Passo 2 — Concorrentes REAIS (não confie nos que o cliente deu)

Erro clássico: assumir que os concorrentes citados são os certos. Pesquise os maiores do ramo na
cidade (`WebSearch`: TeleListas, Econodata, guias locais, "maiores empresas de X em <cidade>").
Depois **separe em dois grupos**:

- **Grupo 1 — pares diretos:** mesmo modelo de negócio e porte. É a comparação que importa.
- **Grupo 2 — adjacentes/varejo:** disputam a mesma demanda por outro ângulo.

Pra cada par direto, cheque a **maturidade digital** (tem loja online? catálogo? Instagram? nota no
Google?). Isso decide o ângulo: se o setor todo é atrasado, o pitch vira *"dá pra ser o primeiro a
liderar"*; se os pares já estão à frente, vira *"você está atrás, precisa correr"*.

## Passo 3 — Análise

**Score de Saúde Digital (0-100).** Sete dimensões, com peso maior pra comércio/conversão:
loja online / vendas digitais · conversão do site · presença social · SEO/achabilidade ·
atendimento & automação · reputação & avaliações · dados & rastreamento. Um número grande na capa
gera urgência. Reputação boa (nota alta) é **ativo subaproveitado**, não problema — reenquadre.

**Vulnerabilidades priorizadas por impacto × esforço.** 4-6 itens, cada um com: o que custa em
dinheiro, e **qual produto/serviço do seu negócio resolve** + se é quick win de 24h. Numere por
prioridade.

**Estimativa de R$ na mesa.** Cenário conservador, **com a conta aberta** (ex.: seguidores ×
conversão % × ticket), rotulado "ilustrativo, a validar com os números reais". Serve pra conversa,
não como promessa.

**Mapa problema → solução.** Cada gargalo apontando pro produto/serviço que fecha.

## Passo 4 — Plano  *(personalize com as suas ofertas)*

- **Quick wins de 24h** (a isca): 3-4 coisas que você entrega rápido e provam valor com risco
  baixo. Exemplos genéricos: automação/atendimento no WhatsApp, instalar pixel + analytics,
  ativar prova social das avaliações, protótipo de catálogo/landing. Troque pelos **seus** serviços.
- **Roadmap 30/60/90** (o upsell): ligar a máquina (loja/site/automação) → trazer demanda
  (SEO/tráfego pago) → automatizar o comercial (qualificação, recompra, dashboard).

---

## Estrutura e design do relatório

Gere um HTML autocontido com a marca **do seu negócio** (é entregável seu, não do cliente).
**Leia `exemplos/exemplo-diagnostico.html`** e siga a mesma estrutura e sistema de design (o
exemplo é um caso real, com dados públicos, só como referência de formato).

Seções, nessa ordem: masthead com o ângulo central + gauge do Score · "diagnóstico em 3 números"
· score por dimensão (barras) · mapa competitivo em 2 grupos (tabelas, com **links** dos
concorrentes no cabeçalho) · vulnerabilidades (cards com faixa de severidade) · oportunidade em R$
(caixa com a conta aberta) · plano de 24h (cards por serviço) · roadmap 30/60/90 · fecho com CTA.

Sistema de design (tokens): um **acento** forte + um secundário + neutros com leve viés no acento
(ajuste às cores da sua marca). Tipografia sã (sans do sistema + mono pra números/labels,
`tabular-nums`). **Sempre com tema claro e escuro** via tokens (`prefers-color-scheme` +
override `data-theme`). Fonte base ~18px pra leitura em tela/projetor (reduz no mobile).

Componentes prontos no exemplo pra reaproveitar: gauge SVG do score, barras de dimensão, tabela
comparativa com coluna "você" destacada, cards de vulnerabilidade com severidade, caixa de R$,
cards de quick win, roadmap em 3 fases, botão-CTA do protótipo.

Salvar em `saidas/diagnostico-<cliente>-<data>.html` (ou na pasta do cliente) e publicar como
**Artifact** pra virar link.

---

## Protótipo ao vivo (opcional, mas fecha negócio)

Quando o diagnóstico aponta falta de loja/app/landing, monte um **protótipo interativo na marca do
cliente** — a prova concreta que vale mais que promessa. Referência: `exemplos/exemplo-loja-demo.html`.

**Extrair a marca do cliente do site dele:**
```
curl -sL -A "Mozilla/5.0" <site> -o home.html
# logo real (não o da agência): grep img com 'logo' no header
grep -oiE '<img[^>]*logo[^>]*>' home.html
# cores: hex e rgb mais frequentes
grep -oiE '#[0-9a-f]{6}' home.html | sort | uniq -c | sort -rn | head
# baixar o logo e amostrar as cores exatas com PIL, depois embutir como data URI base64
```
Embuta o logo como `data:image/png;base64,...` (o CSP do Artifact bloqueia imagem externa). Ponha o
logo numa plaquinha branca pra ficar legível nos dois temas. Refaça a paleta nas cores da marca.

**Funcionalidades que valem no protótipo:** busca por peça/produto e por placa (a placa é só
conveniência — precisa de API paga de consulta; começar por busca por produto, que é grátis),
categorias, carrinho, dados do cliente opcionais (CNPJ/CPF, entrega no endereço cadastrado ou novo),
e **checkout que monta o pedido no WhatsApp**: `https://wa.me/<numero>?text=<pedido>`. Dentro do
Artifact, abrir via `<a>` clicado por código (window.open costuma ser bloqueado). O número não
dispara sozinho — o usuário confere e envia.

**Ligar ao diagnóstico:** botão-CTA no diagnóstico (`.demo-cta`) apontando pro Artifact do
protótipo, pra abrir ao vivo na hora certa da apresentação.

**Cuidado outward-facing:** nunca mande pedido de teste pro WhatsApp real do cliente sem ele saber.
Testar no número do próprio usuário, ou fazer o envio real ao vivo, com o cliente vendo.

---

## Checklist de qualidade

- [ ] Achei o **ângulo central** (o ativo caro que não converte)?
- [ ] Concorrentes são os **reais**, em 2 grupos, com maturidade digital checada?
- [ ] Todo dado não confirmado está como **n/d**; toda estimativa está **rotulada**?
- [ ] Cada vulnerabilidade aponta pra um **produto/serviço seu** e marca se é quick win?
- [ ] Tom de voz do seu negócio (ver `preferencias.md`), sem promessa impossível?
- [ ] Tema claro **e** escuro funcionando? Fonte legível em tela?
- [ ] Salvei em `saidas/`/pasta do cliente e publiquei o Artifact?
