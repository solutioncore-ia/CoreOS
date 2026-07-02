---
name: precificar
description: >
  Ajuda a calcular o preço de um serviço ou produto considerando custo real, tempo investido
  e margem — não achismo nem "preço que o concorrente cobra". Mostra a conta aberta e alerta
  quando o preço proposto pelo usuário fica abaixo do mínimo viável.
  Use quando o usuário disser "quanto cobrar", "precificar", "/precificar", "que preço eu coloco",
  "tá caro ou barato isso", "calcular margem", "quanto vale meu serviço".
---

# /precificar — Cálculo de preço com margem real

Skill pra quem tá decidindo quanto cobrar e só tem "achismo" ou "o que o concorrente cobra" como referência. O objetivo é sempre mostrar a conta aberta, nunca só um número.

## Dependências

- **Contexto do negócio:** `_memoria/empresa.md` (perfil solopreneur/freelancer não tem custo fixo rateado do mesmo jeito que empresa com equipe)
- **Histórico:** `financeiro/precificacao/` (criar se não existir)

---

## Workflow

### Passo 1 — O que está sendo precificado

Perguntar:
1. "O que você quer precificar? (serviço único, serviço recorrente/mensalidade, produto físico, produto digital)"
2. "Você já tem um número em mente, ou parte do zero?"

### Passo 2 — Levantar custos reais

Conforme o tipo, perguntar só o que se aplica:

- **Custo direto:** materiais, ferramentas pagas, terceirizados/freelancers envolvidos nessa entrega específica
- **Tempo investido:** quantas horas essa entrega toma (do início ao fim, incluindo revisão/ajuste), e quanto vale a hora do usuário (se não souber, ajudar a estimar: quanto ele precisa faturar por mês ÷ horas disponíveis)
- **Impostos/taxas:** qual o regime tributário (MEI, Simples Nacional, autônomo) e a alíquota aproximada sobre essa nota/recebimento — esse valor entra no custo, não sai do lucro depois. Se o usuário não souber, perguntar antes de seguir; não assumir alíquota
- **Custo fixo rateado** (só se fizer sentido pro perfil — empresa/agência com estrutura): quanto dos custos fixos mensais (ferramentas, equipe, aluguel) essa entrega deveria carregar

Se o usuário não souber algum número, ajudar a estimar com uma pergunta simples em vez de travar ("quantas horas mais ou menos, no chute?").

### Passo 3 — Calcular as três referências

Imposto incide sobre o valor bruto recebido, não é um custo fixo somado — por isso entra dividindo, não somando (senão o usuário paga imposto sobre o próprio imposto sem perceber):

```
Custo real (líquido) = custo direto + (horas × valor-hora) + rateio de fixo

Preço mínimo viável = custo real ÷ (1 - alíquota)
Preço-alvo          = (custo real × (1 + margem desejada)) ÷ (1 - alíquota)
Teto de mercado      = o que o usuário souber que o mercado paga (se souber)
```

Se o usuário não tiver margem em mente, sugerir 20-40% como faixa comum pra serviço, e perguntar se quer ajustar.

### Passo 4 — Mostrar a conta aberta

```markdown
## Precificação — <item>

**Custo direto:** R$ XXX
**Tempo:** N horas × R$ XX/hora = R$ XXX
**Rateio de fixo:** R$ XXX (se aplicável)
**Custo real (líquido):** R$ XXX
**Alíquota (regime <MEI/Simples/autônomo>):** X%

**Preço mínimo viável:** R$ XXX (cobre custo + imposto, sem lucro)
**Preço-alvo (margem de X%):** R$ XXX
**Teto de mercado:** R$ XXX (se informado)

**Recomendação:** R$ XXX
```

### Passo 5 — Alertar se o número do usuário for baixo

Se na Passo 1 o usuário já tinha um preço em mente e ele ficar abaixo do preço mínimo viável:

> "O preço que você tinha em mente (R$ X) fica abaixo do mínimo viável (R$ Y) — nesse valor você paga o custo mas não sobra nada pro seu tempo. Quer ajustar ou tem algum motivo pra cobrar assim mesmo (ex: cliente estratégico, teste de mercado)?"

Não insistir se o usuário confirmar que é intencional (loss leader, cliente-âncora, etc.) — só registrar o motivo.

### Passo 6 — Salvar

Guardar em `financeiro/precificacao/<item-slug>.md` com a conta completa e a data, pra não precisar recalcular do zero da próxima vez que o mesmo tipo de entrega aparecer.

---

## Regras

- **Nunca dar preço final sem mostrar a conta.** Número solto não ajuda ninguém a confiar na decisão.
- **Faturamento não é lucro.** Se o usuário confundir os dois, apontar a diferença.
- **Perfil muda o cálculo.** Solopreneur/freelancer sem estrutura não tem "rateio de fixo" real — focar em tempo + custo direto + margem.
- **Não inventar valor-hora.** Se o usuário não souber, ajudar a chegar num número com pergunta guiada, não assumir um valor de mercado genérico.
- **Não inventar alíquota.** Se o usuário não souber o regime tributário, perguntar antes de calcular — nunca assumir uma alíquota "padrão", ela muda bastante entre MEI, Simples e autônomo.
