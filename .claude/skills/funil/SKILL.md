---
name: funil
description: >
  Mantém um pipeline simples de vendas — quem foi contatado, em que fase tá, e o que fazer a
  seguir. Adiciona lead novo, atualiza estágio, ou devolve um resumo de "como tão as vendas" e
  quem tá esperando resposta. Use quando o usuário disser "funil", "/funil", "pipeline",
  "quem falta responder", "registra esse lead", "como tão as vendas", "adiciona um cliente
  em prospecção".
---

# /funil — Pipeline de vendas

Conteúdo e ads geram atenção; sem acompanhar quem foi contatado e em que fase tá, essa atenção nunca vira venda. Essa skill é o registro simples que fecha esse elo — não é CRM completo, é uma tabela viva.

## Dependências

- **Arquivo do pipeline:** `vendas/funil.md` — ou `comercial/funil.md` se essa pasta já existir (convenção do perfil empresa)
- **Contexto:** `_memoria/empresa.md` (pra saber o tipo de cliente que o negócio atende)

---

## Onde salvar

Antes de criar o arquivo pela primeira vez, checar se já existe pasta `comercial/` na raiz. Se existir, usar `comercial/funil.md`. Se não, criar `vendas/funil.md`.

## Estrutura do arquivo

```markdown
# Funil de vendas

| Nome | Contato | Estágio | Última ação | Próximo passo | Data prevista |
|---|---|---|---|---|---|
| Acme Ltda | acme@email.com | Proposta enviada | Proposta enviada 12/06 | Follow-up | 19/06 |
```

**Estágios fixos, nessa ordem:**
1. Contato inicial
2. Proposta enviada
3. Negociação
4. Fechado (ganho)
5. Perdido

## Workflow

### Se o usuário quer adicionar um lead novo

Perguntar o que faltar: nome, contato, estágio atual (default "Contato inicial"), próximo passo, data prevista. Adicionar como nova linha na tabela, sem reformatar o resto do arquivo.

### Se o usuário quer atualizar um lead existente

Localizar a linha pelo nome. Atualizar estágio/última ação/próximo passo/data. Se o novo estágio for "Fechado (ganho)", perguntar se quer rodar `/novo-projeto` pra esse cliente.

### Se o usuário pergunta "como tão as vendas" ou pede resumo

Ler o arquivo inteiro e devolver:

```markdown
## Funil — resumo

**Total ativo:** N leads (excluindo Fechado e Perdido)
**Por estágio:** Contato inicial (N) · Proposta enviada (N) · Negociação (N)

**Atrasados** (data prevista já passou e o estágio não mudou):
- [Nome] — devia ter tido [próximo passo] até [data]

**Fechados esse mês:** N (R$ X se houver valor registrado)
```

### Se o usuário pergunta "quem falta responder"

Listar só os leads com `Data prevista` vencida ou vencendo nos próximos 3 dias, ordenado por mais atrasado primeiro.

## Regras

- **Não inventar estágio ou data.** Se o usuário não informar, deixar em branco ou perguntar — nunca assumir "Contato inicial" sem confirmar se já não é outro estágio.
- **Não apagar histórico.** Leads "Perdido" continuam na tabela (não deletar) — é dado útil pra entender padrão de perda depois.
- **Uma linha por lead, sem duplicar.** Se o nome já existir na tabela, atualizar a linha em vez de criar outra.
- **Simplicidade antes de tudo.** Se o usuário pedir campo extra (ex: "valor do contrato", "origem do lead"), adicionar coluna — não travar em rigidez de estrutura.
