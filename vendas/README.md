# vendas/ — pipeline de quem pode virar cliente

Onde mora o `funil.md` mantido pelo `/funil` — um pipeline simples de quem foi contatado, em que fase tá, e o que fazer a seguir. Sem isso, conteúdo e ads geram atenção que ninguém acompanha até virar venda.

## Estrutura padrão

```
vendas/
└── funil.md    lista viva de leads/prospects, uma linha por pessoa/empresa
```

> Se o seu perfil já usa uma pasta `comercial/` (comum no perfil empresa), o `/funil` guarda o pipeline lá dentro em vez de criar `vendas/` — é a mesma função, nome diferente.

## Como funciona

- **`/funil`** → adiciona lead novo, atualiza estágio, lista quem tá esperando resposta, ou dá o resumo de "como tão as vendas"
- Estágios fixos: Contato inicial → Proposta enviada → Negociação → Fechado (ganho) → Perdido

## Versionamento

Fica no git pelo `/salvar`. É dado sensível do negócio (nomes, contatos) — mesmo tratamento que `_memoria/empresa.md` já recebe.
