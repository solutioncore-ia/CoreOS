# Catalogo de Skills

Skills externas prontas pra instalar. Use como referencia ao criar skills novas com `/mapear-rotinas` ou instale diretamente as que fizerem sentido pro seu negocio.

> Skills globais ficam em `~/.claude/skills/` e funcionam em qualquer projeto.
> Skills locais ficam em `.claude/commands/` e so funcionam nesse projeto.

> Schwartz Copy, Ogilvy Copy, GA4 CoreOS, Meta Ads CoreOS, Google Ads CoreOS
> e Ads CoreOS ja vem instaladas por padrao em `.claude/skills/` — nao
> precisam ser buscadas aqui. As quatro ultimas exigem configurar
> credencial de API (token Meta, developer token Google Ads, service
> account GA4) antes de funcionar; rode o `setup` de cada uma quando
> tiver a primeira conta de cliente pra conectar. Veja o passo a passo
> completo em "Anúncios pagos — setup" no README.

---

## Criar interfaces e paginas web

### Frontend Design
**O que faz:** Cria interfaces web completas com design de alta qualidade. Gera codigo HTML/CSS/React pronto pra usar, com visual profissional que foge da estetica generica de IA.
**Bom pra:** Landing pages, dashboards, componentes web, paginas de produto
**Como instalar:** Ja vem nativo no Claude Code. Chamar com `/frontend-design`
**Fonte:** Skill nativa do Claude Code

---

## Criar visuais e arte

### Canvas Design
**O que faz:** Cria arte visual em PNG e PDF usando principios de design. Posters, capas, pecas graficas.
**Bom pra:** Capas de ebook, banners, pecas visuais, thumbnails
**Como instalar:** Ja vem nativo no Claude Code. Chamar com `/canvas-design`
**Fonte:** Skill nativa do Claude Code

---

## Trabalhar com documentos

### PDF
**O que faz:** Manipula PDFs: extrai texto e tabelas, cria novos, junta/separa documentos, preenche formularios.
**Bom pra:** Extrair dados de contratos, criar relatorios em PDF, preencher formularios
**Como instalar:** Ja vem nativo no Claude Code. Chamar com `/pdf`
**Fonte:** Skill nativa do Claude Code

### DOCX
**O que faz:** Cria e edita documentos Word com formatacao, tracked changes e comentarios.
**Bom pra:** Propostas formais, contratos, documentos pra clientes que pedem Word
**Como instalar:** Ja vem nativo no Claude Code. Chamar com `/docx`
**Fonte:** Skill nativa do Claude Code

### PPTX
**O que faz:** Cria e edita apresentacoes PowerPoint com layouts, speaker notes e formatacao.
**Bom pra:** Apresentacoes pra clientes, decks de vendas, materiais de treinamento
**Como instalar:** Ja vem nativo no Claude Code. Chamar com `/pptx`
**Fonte:** Skill nativa do Claude Code

### XLSX
**O que faz:** Cria e edita planilhas com formulas, formatacao e graficos.
**Bom pra:** Relatorios financeiros, dashboards em planilha, analise de dados
**Como instalar:** Ja vem nativo no Claude Code. Chamar com `/xlsx`
**Fonte:** Skill nativa do Claude Code

---

## Escrever documentos e specs

### Doc Co-Authoring
**O que faz:** Fluxo guiado pra coescrever documentos. Te entrevista, itera rascunhos, e valida que o documento funciona pro leitor.
**Bom pra:** Propostas tecnicas, specs, documentos de decisao, SOPs
**Como instalar:** Ja vem nativo no Claude Code. Chamar com `/doc-coauthoring`
**Fonte:** Skill nativa do Claude Code

---

## Extrair transcricao de video

### YT Transcript
**O que faz:** Extrai transcricoes de videos do YouTube usando yt-dlp. Suporta multiplos idiomas.
**Bom pra:** Criar conteudo a partir de videos (carrosseis, newsletters, posts)
**Precisa de:** yt-dlp instalado (`brew install yt-dlp`)
**Como instalar:** Ja vem como skill global. Chamar com `/yt-transcript`
**Fonte:** Skill validada pelo CoreOS

---

## Testar sites e apps

### Webapp Testing
**O que faz:** Testa aplicacoes web locais usando Playwright. Captura screenshots, verifica funcionalidade, le logs do browser.
**Bom pra:** Testar landing pages antes de publicar, verificar se tudo funciona em diferentes tamanhos
**Como instalar:** Ja vem nativo no Claude Code. Chamar com `/webapp-testing`
**Fonte:** Skill nativa do Claude Code

---

## Criar skills novas

### Skill Creator
**O que faz:** Guia pra criar skills novas do zero. Ajuda a estruturar, definir triggers, e testar.
**Bom pra:** Quando o `/mapear-rotinas` nao cobre o que voce precisa e quer criar algo mais complexo
**Como instalar:** Ja vem nativo no Claude Code. Chamar com `/skill-creator`
**Fonte:** Skill nativa do Claude Code

---

## Como adicionar skills novas a este catalogo

Se voce testou uma skill e quer adicionar aqui pra referencia futura:

```markdown
### Nome da Skill
**O que faz:** [descricao em uma frase]
**Bom pra:** [casos de uso praticos]
**Como instalar:** [comando ou instrucao]
**Fonte:** [de onde veio — skill nativa, criada por voce, ou de terceiros]
```
