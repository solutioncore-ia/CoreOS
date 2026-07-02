---
name: financeiro
description: >
  Lê extratos bancários, notas fiscais ou lançamentos soltos (CSV, PDF ou colados em texto)
  da pasta `dados/` e devolve um DRE simples — quanto entrou, quanto saiu, categorizado, e quanto
  sobrou. Compara com o mês anterior e alerta sobre saldo negativo ou categoria de custo crescendo
  fora do padrão. Use quando o usuário disser "financeiro", "/financeiro", "como tá o caixa",
  "fecha o mês", "quanto sobrou", "extrato", "balanço do mês".
---

# /financeiro — Raio-x financeiro do mês

Transforma extrato bruto em resposta pra pergunta que todo dono de negócio leigo tem e não sabe responder: "no fim do mês, sobrou dinheiro ou não?"

## Dependências

- **Contexto:** `_memoria/empresa.md`, `_memoria/estrategia.md`
- **Inputs:** extrato bancário (CSV/PDF/print), notas fiscais, ou lançamentos colados em texto livre — de `dados/`
- **Histórico:** `financeiro/relatorios/` (criar se não existir)

---

## Como rodar

```
/financeiro
dados/extrato-junho.csv
```

Ou sem arquivo — o usuário pode colar os lançamentos direto no chat ("recebi R$ 2000 do cliente X dia 5, paguei R$ 300 de ferramenta dia 8...").

## Workflow

### Passo 1 — Ler e categorizar

Ler os lançamentos e classificar cada um em:

**Entradas:** por cliente/fonte (ex: "Cliente Acme", "Venda produto X")
**Saídas**, agrupadas em categorias simples:
- Ferramentas/assinaturas
- Impostos
- Equipe/terceirizados
- Marketing/ads
- Operacional (aluguel, contas fixas)
- Outros

Se um lançamento for ambíguo, perguntar em vez de adivinhar a categoria.

### Passo 2 — Calcular o resultado do mês

```
Total de entradas:  R$ X
Total de saídas:    R$ Y
Saldo do mês:        R$ X - Y
```

### Passo 3 — Comparar com o mês anterior

Buscar em `financeiro/relatorios/` o DRE do mês anterior. Se existir, calcular variação:
- Entradas (▲/▼ %)
- Saídas totais (▲/▼ %)
- Saldo (▲/▼ %)
- Categoria de saída que mais cresceu em proporção

Se não existir, é a primeira leitura — sinalizar como baseline.

### Passo 4 — Resumo executivo

```markdown
# Raio-x financeiro — <mês/ano>

**Entrou:** R$ X.XXX (▲/▼ Y% vs mês anterior)
**Saiu:** R$ X.XXX (▲/▼ Y%)
**Sobrou:** R$ X.XXX

**Maior fonte de entrada:** [cliente/fonte]
**Maior categoria de saída:** [categoria] — R$ X.XXX

**Headline do mês:** 1 frase do que mais importa (saldo apertando, categoria de custo disparando, mês recorde).
```

### Passo 5 — Alertas

| Alerta | Critério |
|---|---|
| 🔴 Saldo negativo | Saiu mais do que entrou |
| 🔴 Categoria disparando | Alguma categoria de saída cresceu >30% vs mês anterior sem explicação óbvia |
| 🟡 Concentração de risco | Mais de 50% das entradas vêm de um único cliente/fonte |
| 🟡 Sem margem de segurança | Saldo positivo mas menor que 10% das entradas |
| 🟢 Saudável | Saldo positivo e estável ou crescendo mês a mês |

### Passo 6 — Recomendações

Lista curta (2-4 itens) de ações concretas, não genéricas:

```markdown
## Pra próximo mês

1. **Renegociar ou cancelar** [ferramenta/assinatura específica] — cresceu X% sem justificativa clara
2. **Diversificar entrada** — [cliente] responde por Y% do faturamento, risco se ele sair
3. **Guardar reserva** — saldo tá positivo mas sem margem, considerar deixar R$ X de lado
```

### Passo 7 — Salvar

```
financeiro/relatorios/<YYYY-MM>-dre.md
```

Frontmatter:
```yaml
---
mes: YYYY-MM
entradas_total: 0000.00
saidas_total: 0000.00
saldo: 0000.00
---
```

---

## Regras

- **Nunca inventar número.** Se um lançamento não ficar claro, perguntar ou marcar como "não categorizado" em vez de chutar.
- **Faturamento ≠ lucro ≠ caixa.** Se o usuário confundir os três, explicar a diferença de forma simples, sem virar aula de contabilidade.
- **Linguagem do dono.** Nada de "EBITDA" ou "DRE gerencial" sem explicar — falar "quanto sobrou" antes de qualquer termo técnico.
- **Comparação é o que importa.** Um número solto não diz se o negócio tá indo bem ou mal — sempre situar contra o mês anterior.
- **Alerta não é acusação.** Reportar problema de forma direta, mas sem alarmismo — "essa categoria dobrou" é mais útil que "cuidado, gastos fora de controle".
