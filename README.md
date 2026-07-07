# CoreOS

> O sistema operacional do seu negócio dentro do Claude Code.

Você acaba de instalar o CoreOS. Em alguns minutos, sua empresa vai
ter uma memória própria, uma identidade visual aplicada em tudo que
o sistema gerar, e 24 skills prontas pra fazer marketing, SEO, copy,
ads, dinheiro, vendas e operação rodarem com você dirigindo.

Bora voar.

---

## Ligando o sistema

Dois caminhos. Escolhe o que combina contigo.

### Pelo Claude (mais rápido)

Abre o Claude Code em qualquer pasta e cola:

```
Clona o https://github.com/solutioncore-ia/CoreOS.git na pasta atual,
entra nela e roda o /instalar.
```

Ele clona, entra na pasta nova e dispara a entrevista de setup. Você
só responde.

### Pelo terminal (mais previsível)

```
git clone https://github.com/solutioncore-ia/CoreOS.git
cd CoreOS
code .
```

Na janela do VS Code que abrir: terminal integrado → `claude` → `/instalar`.

---

Quando o `/instalar` terminar, renomeia a pasta `CoreOS/` pro nome do teu
negócio (fecha o VS Code, renomeia no Explorer/Finder, abre de novo). A
pasta não fica como "CoreOS" — ela é o teu negócio agora.

O `/instalar` roda uma vez só. Te entrevista sobre o negócio, monta a
memória e configura o sistema. Depois disso, é só usar.

---

## O sistema

**Núcleo** — o jeito de operar o dia a dia
`/abrir` carrega o contexto antes de cada sessão de trabalho · `/salvar`
faz commit + push no GitHub · `/atualizar` varre o projeto e atualiza
a memória · `/novo-projeto` cria pasta isolada pra cada cliente ou
iniciativa · `/mapear-rotinas` descobre o que você repete e transforma
em skill personalizada.

**Dinheiro e vendas** — saber se o negócio é viável e fechar venda
`/precificar` calcula preço de serviço/produto com margem real, mostrando
a conta aberta · `/financeiro` lê extrato/notas e devolve um raio-x
simples de quanto entrou, saiu e sobrou no mês · `/funil` mantém o
pipeline de vendas — quem foi contatado, em que fase tá, o que fazer
a seguir.

**Conteúdo e SEO** — vitrine pública da empresa
`/carrossel` cria carrosséis 1080×1350 com identidade da marca (com ou
sem foto IA) · `/publicar-tema` pega um tema e entrega artigo de blog +
carrossel + 3 legendas amarradas · `/seo` roda fluxo completo de 8 passos
(demanda, concorrência, GMB, on-page, conteúdo, ads, monitoramento, GEO)
· `/responder-avaliacoes` escreve respostas humanas pras reviews do
Google · `/aprovar-post` publica blog + Instagram + Facebook num comando.

**Copywriting** — texto que vende ou constrói marca
`/schwartz-copy` gera copy de resposta direta (landing pages, emails,
VSLs) diagnosticando nível de consciência e sofisticação do mercado
antes de escrever · `/ogilvy-copy` gera copy institucional e de
posicionamento de marca (manifestos, campanhas, taglines, brand voice).

**Anúncios pagos** — onde o dinheiro entra
`/anuncio-google` monta a campanha inteira em CSV pronto pra importar
no Google Ads Editor, sem precisar de credencial de API · `/relatorio-ads`
lê exports em CSV de Google + Meta e devolve relatório semanal com
alertas e recomendações · `/meta-ads-coreos` e `/google-ads-coreos`
executam direto via API oficial — criam, editam, pausam e duplicam
campanhas de verdade (setup de token/OAuth por conta) · `/ga4-coreos`
consulta o Google Analytics 4 — sessões, conversões, fontes de tráfego,
tempo real · `/ads-coreos` é a camada de inteligência acima dos três:
Health Score, benchmarks do mercado brasileiro e Quality Gates pra
diagnóstico e auditoria.

**Produção** — ferramentas do dia a dia
`/analisar-dados` lê CSV/XLSX/PDF e gera resumo executivo ·
`/email-profissional` rascunha email a partir de contexto livre.

---

## Anúncios pagos — setup das skills com API

`meta-ads-coreos`, `google-ads-coreos`, `ga4-coreos` e `ads-coreos` já
vêm instaladas em `.claude/skills/`, mas dependem de credencial de API
por conta — não funcionam sozinhas até você configurar. `/anuncio-google`
e `/relatorio-ads` continuam funcionando sem nenhum setup (CSV manual),
use-os enquanto não configurar as de API.

**Ordem recomendada, na primeira vez que for gerenciar tráfego pago de
um cliente:**

1. **Configure a plataforma que o cliente usa.** Rode `/meta-ads-coreos setup`
   (Meta/Instagram) e/ou `/google-ads-coreos setup` (Google Search/PMax).
   Cada uma te guia pra gerar o token certo e cadastra a conta do cliente
   num `contas.yaml` próprio.
2. **Opcional — analytics do site do cliente:** `/ga4-coreos setup` (aceita
   reusar a credencial OAuth do Google Ads se ela já estiver configurada).
3. **Use direto** as skills de execução pra ler campanhas, criar anúncios
   (sempre nascem pausados, por segurança) ou puxar métricas — é só pedir
   em linguagem natural ("cria uma campanha de leads pro Cliente X",
   "métricas dos últimos 7 dias").
4. **Quando tiver pelo menos uma conectada**, `/ads-coreos setup` habilita
   o diagnóstico — `/ads-coreos diagnostico` (check rápido), `/ads-coreos relatorio`
   (dashboard HTML pro cliente) e `/ads-coreos auditoria` (revisão mensal
   com Quality Gates e benchmarks BR).

Sem credencial configurada, essas quatro skills ficam inertes — não
atrapalham nada, só não fazem nada até você rodar o setup.

---

## A tese

IA não é uma ferramenta que sua empresa usa. É o sistema operacional em
que ela roda.

A diferença não é velocidade. É capacidade nova — uma pessoa com IA
constrói o que antes exigia time inteiro. Cada processo crítico que hoje
roda em open loop (decide → executa → não mede → repete cego) vira
closed loop dentro do CoreOS (decide → executa → captura → realimenta →
ajusta sozinho).

O sistema não substitui você. Vira parte da sua empresa.

---

## Como o CoreOS pensa

`_memoria/` é o cérebro. Tudo que importa do seu negócio mora aqui —
quem é a empresa, como ela fala, o que tá em foco essa semana. O Claude
lê isso antes de cada resposta. Quanto melhor a memória, melhor o sistema.

`identidade/` é o rosto. Cores, fontes, logo, padrão visual. Todo
carrossel, slide, peça que o sistema gera respeita isso.

`marketing/`, `saidas/`, `financeiro/`, `vendas/` e `scripts/` são o
resultado. O sistema produz, versiona no GitHub, fica tudo seu.
