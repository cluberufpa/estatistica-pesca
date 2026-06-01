# Estatística Aplicada à Pesca e Aquicultura — Web-book

Guia de estudo da disciplina **EP05042** (45 h), Bacharelado em Engenharia de Pesca, UFPA — Campus Bragança (FEPESCA / IECOS). Construído em [Quarto](https://quarto.org) com saída **HTML** (GitHub Pages) e **PDF via Typst**.

## O que é isto

Um web-book que integra os três pilares da disciplina — **Planejamento**, **Análise com R** e **Comunicação** — com apoio consciente de IA (Posit Assistant). Serve de guia de estudo, referencia os livros da ementa, embute os vídeos do YouTube e traz os desafios com dados.

## Pré-requisitos (na sua máquina)

1. [R](https://cran.r-project.org/) (instale primeiro)
2. [RStudio](https://posit.co/download/rstudio-desktop/)
3. [Quarto](https://quarto.org/docs/get-started/) (≥ 1.4, com suporte a Typst)
4. Pacotes R: `install.packages(c("tidyverse","readxl","car","knitr","rmarkdown"))`

> Typst já vem embutido no Quarto recente — não precisa instalar LaTeX.

## Como visualizar localmente

```bash
quarto preview        # abre no navegador e recarrega ao salvar
quarto render         # gera tudo em /docs
quarto render --to html     # só o site
quarto render --to typst    # só o PDF
```

## Como publicar no GitHub Pages

1. Crie um repositório no GitHub (ex.: `estatistica-pesca`) e suba estes arquivos.
2. Edite `_quarto.yml`: troque `SEU_USUARIO` em `site-url` e `repo-url`.
3. Em **Settings → Pages**, defina a fonte como **GitHub Actions** (ou branch `gh-pages`).
4. A cada `git push` na branch `main`, o workflow `.github/workflows/publish.yml` renderiza e publica automaticamente.

## O que personalizar

| Onde | O quê |
|---|---|
| `_quarto.yml` | nome do autor, URLs do GitHub |
| `referencias.bib` | **os livros exatos da sua ementa** (os atuais são modelos) |
| `capitulos/*.qmd` | trocar `SEU_VIDEO_ID` pelos vídeos reais do seu canal |
| `figuras/` | adicionar `capa.png` e `favicon.png` |
| `dados/` | acrescentar os datasets dos demais desafios |

## Estrutura

```
.
├── _quarto.yml          ← configuração do book (HTML + Typst)
├── estilo.scss          ← tema visual institucional FEPESCA
├── index.qmd            ← abertura: pacto de IA e os 3 pilares
├── capitulos/           ← 14 capítulos (Fundamentos + 3 pilares + Desafios)
├── dados/               ← datasets dos desafios
├── referencias.bib      ← bibliografia da ementa
├── references.qmd
└── .github/workflows/   ← publicação automática
```

## Princípio pedagógico

> **A IA escreve o código. Você valida os pressupostos e interpreta.**

Todo o material reforça essa ideia: a competência avaliada não é digitar R (a IA faz), mas julgar se a análise é válida e o que ela significa para a biologia da pesca.
