# Ads CoreOS

Inteligência de tráfego pago para Claude Code. Diagnóstico, relatório, auditoria e estratégia para Meta Ads e Google Ads com benchmarks do mercado brasileiro.

## Instalação

Já vem instalada por padrão em `.claude/skills/ads-coreos/` em qualquer negócio criado com o CoreOS.

## Pré-requisitos

Precisa de credencial configurada em pelo menos uma skill de execução (já instaladas junto, faltando só o setup de token/OAuth):

- **Meta Ads**: `.claude/skills/meta-ads-coreos/` — rodar `/meta-ads-coreos setup`
- **Google Ads**: `.claude/skills/google-ads-coreos/` — rodar `/google-ads-coreos setup`
- **GA4**: `.claude/skills/ga4-coreos/` — rodar `/ga4-coreos setup`

## Setup

```
/ads-coreos setup
```

Guia o cadastro de contas e testa conexões.

## Comandos

| Comando | O que faz | Quando usar |
|---|---|---|
| `/ads-coreos setup` | Configura contas e testa conexões | Primeira vez |
| `/ads-coreos diagnostico` | Health Score + KPIs + alertas automáticos | Check diário (5 min) |
| `/ads-coreos relatorio` | Dashboard HTML com benchmarks BR | Entrega pro cliente |
| `/ads-coreos auditoria` | Análise profunda com Quality Gates | Revisão mensal |

## O que está incluso

- **Benchmarks BR**: métricas de referência do mercado brasileiro por nicho
- **Quality Gates**: regras de decisão (3x Kill Rule, limites de escala, bidding)
- **Health Score**: nota 0-100 da conta com classificação A-F
- **Alertas automáticos**: detecção de problemas com números e ações

## Arquitetura

```
ads-coreos (cérebro — estratégia + inteligência)
  ├── referencia → meta-ads-coreos (execução Meta)
  ├── referencia → google-ads-coreos (execução Google)
  └── referencia → ga4-coreos (execução Analytics)
```

## Licença

MIT — [Ratos de IA](https://ratosdeia.com.br)
