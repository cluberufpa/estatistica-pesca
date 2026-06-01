# Primeiros passos — render local e publicação

Guia rápido para tirar o web-book do papel. Siga **nesta ordem**.

---

## Etapa 1 — Testar no seu computador (antes de qualquer GitHub)

1. Abra o arquivo **`webbook.Rproj`** no RStudio (duplo clique). Isso abre o projeto e ajusta o diretório de trabalho automaticamente.

2. Instale os pacotes que os capítulos usam (uma vez só). No **Console** do RStudio:

   ```r
   install.packages(c("tidyverse", "readxl", "car", "knitr", "rmarkdown"))
   ```

3. Baixe o estilo de citação ABNT (uma vez só). No **Terminal** do RStudio, dentro da pasta `webbook`:

   ```bash
   curl -L -o abnt.csl https://raw.githubusercontent.com/citation-style-language/styles/master/associacao-brasileira-de-normas-tecnicas.csl
   ```

   Isso cria o arquivo `abnt.csl` na pasta. O `_quarto.yml` já aponta para ele.
   *(Se não quiser citações em ABNT agora, abra `_quarto.yml` e comente a linha `csl: abnt.csl` colocando um `#` na frente.)*

4. Confira se o Quarto enxerga o Typst (no **Terminal** do RStudio — a aba ao lado do Console):

   ```bash
   quarto --version
   quarto check
   ```

5. Renderize o site inteiro:

   ```bash
   quarto render
   ```

   Se tudo der certo, aparece uma pasta **`docs/`** com o site. Abra `docs/index.html` no navegador para ver.

6. Para trabalhar com pré-visualização ao vivo (recarrega ao salvar):

   ```bash
   quarto preview
   ```

> **Se der erro:** quase sempre é um pacote faltando — a mensagem diz qual. Instale com `install.packages("nome")` e rode de novo. Resolva tudo aqui, offline, antes da Etapa 2.

---

## Etapa 2 — Criar o repositório no GitHub

1. Em **github.com/cluberufpa**, clique em **New repository**.
2. Nome sugerido: `estatistica-pesca`.
3. Visibilidade: **Public** (necessário para o GitHub Pages gratuito).
4. **NÃO marque** "Add a README", ".gitignore" nem "license" — o repositório precisa nascer **vazio**, porque o conteúdo já está no seu computador.
5. Clique em **Create repository**. Anote a URL que aparece:
   `https://github.com/cluberufpa/estatistica-pesca.git`

---

## Etapa 3 — Conectar o computador ao GitHub

⚠️ **Onde rodar:** no **Terminal do RStudio**, dentro da pasta do web-book
(`D:\EP05042-Estatistica-Pesca\webbook`) — **não** na pasta-mãe.

Confirme que está na pasta certa (deve listar `_quarto.yml`):

```bash
ls          # ou, no Windows: dir
```

Depois, uma vez só:

```bash
git init
git add .
git commit -m "Primeira versao do web-book"
git branch -M main
git remote add origin https://github.com/cluberufpa/estatistica-pesca.git
git push -u origin main
```

> Na primeira vez o Git pode pedir login. Use seu usuário do GitHub e um **token de acesso** (Settings → Developer settings → Personal access tokens) no lugar da senha — o GitHub não aceita mais senha pura no push.

---

## Etapa 4 — Ligar o GitHub Pages

1. No repositório, vá em **Settings → Pages**.
2. Em **Build and deployment → Source**, escolha **GitHub Actions**.
3. O workflow `.github/workflows/publish.yml` (já incluso) renderiza e publica a cada `push`.
4. Em alguns minutos o site fica no ar em:
   `https://cluberufpa.github.io/estatistica-pesca/`
5. Ajuste essa URL em **`_quarto.yml`** (campos `site-url` e `repo-url`, troque `SEU_USUARIO` por `cluberufpa`).

---

## O ciclo do dia a dia (depois de tudo pronto)

Sempre que mudar um capítulo, adicionar um vídeo ou um dataset:

```bash
git add .
git commit -m "descreva a mudanca aqui"
git push
```

O Actions republica sozinho. Você nunca precisa renderizar à mão para publicar — só para conferir localmente com `quarto preview`.

---

## O que vai (e o que NÃO vai) para o GitHub

```
EP05042-Estatistica-Pesca/        ← pasta central (NÃO é repositório)
├── webbook/        ←★ SÓ ESTA pasta vira o repositório Git/GitHub
├── apresentacoes/   ← fica no seu PC, privado
├── videos-roteiros/ ← fica no seu PC, privado
└── administrativo/  ← fica no seu PC, privado
```

O `git init` acontece **dentro de `webbook/`**. As outras pastas ficam organizadas ao lado, mas não são publicadas.
