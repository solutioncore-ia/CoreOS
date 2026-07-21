# Playbook — Postagem automática (Instagram + blog)

> **Leia ANTES de ligar a postagem automática em qualquer cliente.**
> Escrito a partir da primeira implantação real em produção (18–21/07/2026), incluindo os
> erros que queimaram uma semana inteira de calendário editorial de um cliente.
> Cada item aqui é um problema que **aconteceu de verdade** — não é precaução teórica.

---

## O incidente que originou este documento

Enfileiramos 6 peças de uma vez (calendário de 8 dias). O publicador do CorePV postou
**5 delas em 2 dias**, de hora em hora. A semana inteira de conteúdo queimou; o cliente
teve que pausar a 6ª manualmente, com o Chrome já abrindo pra postar.

**Causa raiz: assumimos que a fila era uma agenda. Ela é uma esteira.**

---

## 1. ⚠️ A fila do publicador é ESTEIRA, não agenda

**O erro mais caro. Entenda isso antes de qualquer outra coisa.**

O publicador do CorePV pega **o próximo item da fila** a cada `intervalo_minutos`, dentro
da janela `instagram.publicar`, e posta **na hora**. Ele **NÃO lê a data/hora do nome da
pasta** — o prefixo `YYYY-MM-DD_HHMM_` que o `enfileirar.mjs` escreve é, pra ele,
decorativo.

Com janela 07:00–21:00 e intervalo de 60min, isso são **até 14 posts por dia**.

### As duas travas obrigatórias (aplicar as DUAS)

**Trava 1 — no dashboard do CorePV, no tenant do cliente:**
```yaml
instagram:
  publicar:
    janela_inicio: 07:00
    janela_fim: 07:59      # 1 slot só → no máximo 1 post/dia
    intervalo_minutos: 60
```

**Trava 2 — na skill de abastecimento do cliente:**
- A fila é **slot único**: havendo qualquer pasta pendente, **não enfileirar nada**
- Enfileirar **uma peça por rodada**, e só a do **próximo slot devido**
- **Nunca** enfileirar peça de data futura além do próximo slot
- Produzir com antecedência é OK (fica em `marketing/conteudo/`); **encher a fila não é**

> Uma trava sozinha já evita o desastre — aplique as duas mesmo assim: uma protege a
> outra caso alguém alargue a janela no dashboard depois.

---

## 2. Cuidado com a ordem: produção x janela de publicação

Se a produção diária roda **depois** que a janela de publicação fechou (ex.: produção
08:00, janela até 07:59), então **o que entra na fila hoje só é publicado amanhã**. A
skill precisa enfileirar **D+1**, não D.

Se você mudar qualquer um dos dois horários, **recalcule essa regra** — ela depende de
qual roda primeiro. Enfileirar "a peça de hoje" nesse arranjo atrasa tudo em um dia.

---

## 3. O `config.yaml` do tenant é espelho — editar local não adianta

O agente rebaixa o config da VPS a cada ~30s e **sobrescreve o arquivo local**. Toda
mudança de janela/intervalo/ativo é feita **no dashboard**. Depois, confirme que desceu
lendo o `config.yaml` do tenant na máquina.

---

## 4. Não confie no registro local de "sucesso"

Na primeira implantação, **5 peças marcadas "sucesso" registraram apenas 3 shortcodes
distintos** do Instagram (`publicado.json` com URL repetida). O registro de URL do
publicador não é confiável como prova.

**Sempre confira o feed real da conta** antes de concluir que algo publicou — ou não.

---

## 5. Ordem correta de implantação num cliente novo

1. **Trave a janela do publicador primeiro** (1 disparo/dia), ANTES de enfileirar
   qualquer coisa. Não deixe pra depois.
2. Clone o repo do cliente e instale as dependências (Node, ffmpeg, playwright, Claude CLI)
3. Configure o `.env` (Telegram, caminho real da fila do tenant)
4. **Configure a identidade do git** (`user.name` e `user.email`) — sem isso o commit
   diário da skill falha; com a identidade errada, o deploy do site é recusado (ver §7)
5. Agende a produção diária
6. **Enfileire UMA peça** e acompanhe o primeiro post ao vivo, supervisionado
7. Só então deixe rodar sozinho

---

## 6. Armadilhas de GitHub e token

- **Token fine-grained não serve.** Mesmo marcado "All repositories", ele não enxergou
  um repo privado da própria conta (404 na API; no clone, a mensagem enganosa
  *"Write access to repository not granted"*). Use **token clássico** com escopo **`repo`**.
- Pra versionar automação (`.github/workflows/`), o token precisa **também** do escopo
  **`workflow`** — senão o push é recusado.
- **O repo do site precisa estar numa conta que o cliente ADMINISTRA.** Com permissão
  apenas de `push` (colaborador em org de terceiro), é impossível configurar: deploy key,
  webhook, secrets de Actions e app do GitHub — **todos exigem admin**. Na primeira
  implantação foi necessário mover o site pra conta do próprio dono.
- **404 no navegador em repo que existe = está logado na conta errada.** Acontece muito:
  clientes costumam ter duas identidades (pessoal e da empresa).

---

## 7. Armadilhas de deploy do site (Netlify)

- **O plano free bloqueia build disparado por git de "contribuidor não verificado".**
  Com conexão por **deploy key**, o Netlify não verifica NENHUM commit → **todo build
  falha**. Sintoma: `Build blocked: unrecognized Git contributor`.
- **Build hook NÃO contorna** (ele builda o último commit, que segue não verificado).
  Webhook de push também não.
- **Solução que funciona: GitHub Actions.** Build em `ubuntu-latest` +
  `netlify deploy --build --prod` (deploy pela API, que não passa por essa checagem).
  Secrets no repo: `NETLIFY_AUTH_TOKEN` e `NETLIFY_SITE_ID`.
- **Não builde Next.js no Windows.** O `@netlify/plugin-nextjs` falha ao empacotar o
  middleware como edge function (`Cannot find module './...-runtime.js'`) — tanto em
  Turbopack quanto em webpack. No Linux funciona: mais um motivo pro build ficar no Actions.

---

## 8. Checklist antes de dar "pronto"

- [ ] Janela do publicador permite **no máximo 1 post/dia**
- [ ] Skill enfileira **1 peça, do próximo slot, só com a fila vazia**
- [ ] `git user.name` / `user.email` configurados (teste: faça um commit)
- [ ] Telegram entregando — mande um teste e **confirme com o cliente que ele viu**
      (não basta a API responder `ok: true`)
- [ ] Primeiro post ao vivo **supervisionado**, com o feed real conferido
- [ ] Se tem blog: um artigo publicado de verdade, deploy concluído, **URL aberta**
- [ ] Máquina do cliente: ligada, logada, **sem suspensão do Windows** — o publicador
      abre um Chrome real
- [ ] Sessão do Instagram ativa no perfil de Chrome do tenant

---

## 9. Regras de calendário que evitam retrabalho

- Sábado costuma ser **curadoria/repost manual** — a fábrica não produz
- Domingo normalmente não tem slot
- Se um dia passa em branco, **a peça daquele dia é perdida, não empurrada** (a skill
  enfileira por data). Pra empurrar, ajuste o calendário explicitamente.
- Não produza muito além de 2 dias à frente: conteúdo parado envelhece e, se a trava da
  fila falhar, vira munição pra um novo incidente.

---

## Resumo em uma frase

**A fila é uma esteira: coloque uma peça por vez, no dia certo, e trave a janela do
publicador em um disparo diário.** Todo o resto é detalhe de execução.
