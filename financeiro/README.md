# financeiro/ — saúde financeira do negócio

Onde ficam os raios-x financeiros gerados pelo `/financeiro` e as decisões de preço geradas pelo `/precificar`. Sem isso, conteúdo e ads podem estar rodando bem enquanto o caixa afunda sem ninguém perceber.

## Estrutura padrão

```
financeiro/
├── relatorios/                   saídas do /financeiro
│   └── <YYYY-MM>-dre.md          entradas, saídas, saldo do mês
│
└── precificacao/                 saídas do /precificar
    └── <item>.md                 memória de como o preço de cada serviço/produto foi calculado
```

## Como funciona

- **`/financeiro`** → lê extratos/notas soltos em `dados/` e devolve um DRE simples em `relatorios/<YYYY-MM>-dre.md`
- **`/precificar`** → calcula preço com margem real e guarda o cálculo em `precificacao/<item>.md`, pra não precisar refazer a conta do zero da próxima vez

## Versionamento

Fica tudo no git pelo `/salvar`. Útil pra comparar mês a mês e ver se o negócio tá saudável ou só parecendo ativo.
