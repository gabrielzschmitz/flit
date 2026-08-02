# FLit

<img align="right" width="192px" src="./icons/logo.svg" alt="FLit Logo">

<a href="./LICENSE"><img src="https://img.shields.io/badge/license-CC%20BY%204.0-lightgreen" alt="Licença"></a>
<a href="https://www.buymeacoffee.com/gabrielzschmitz" target="_blank"><img src="https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png" alt="Buy Me A Coffee" style="height: 20px !important;width: 87px;"></a>
<a href="https://github.com/gabrielzschmitz/flit"><img src="https://img.shields.io/github/stars/gabrielzschmitz/flit?style=social" alt="Deixe uma estrela"></a>

**FLit** é um conjunto de materiais de formação literária produzidos em LaTeX.
O projeto reúne textos de apoio para o estudo da literatura, como comentários
críticos, análises de obras e outros materiais didáticos, desenvolvidos com
foco em clareza, organização e fundamentação em fontes originais.

A produção é organizada em categorias, cada uma contendo estudos individuais.
Cada estudo é um projeto LaTeX autônomo segue o mesmo padrão: `main.tex` +
`style.sty` + `sections/` + `ref.bib`.

---

## Compilação

Cada estudo, independentemente da categoria, é um projeto LaTeX autônomo,
compilado com **latexmk** (pdfLaTeX + BibTeX).

<details>
<summary>Compilar do código</summary>

```bash
latexmk -pdf -f -bibtex main.tex
```
</details>

<details>
<summary>Usando os scripts auxiliares (preferível)</summary>

Copie `texcomp` e `latexide` (quando presentes na pasta do estudo) para a
raiz do estudo e execute a partir de lá. `texcomp` compila uma vez e organiza
os arquivos auxiliares em `.aux/`:

```bash
./texcomp main.tex
```

`latexide` abre um ciclo de visualização ao vivo (`st` + `entr` + `zathura` +
`nvim`):

```bash
./latexide main.tex
```
</details>

<details>
<summary>Limpeza</summary>

Os arquivos auxiliares são ignorados pelo `.gitignore`; os PDFs são
rastreados com **Git LFS** (veja `.gitattributes`).

```bash
latexmk -c           # remove arquivos auxiliares
rm -rf .aux          # limpa o diretório auxiliar organizado
```
</details>

---

## Uso

O PDF resultante (`main.pdf`) é um documento A4 pronto para impressão, com
página de capa, o conteúdo organizado em seções, figuras e uma bibliografia
numérica. A capa é gerada pelo comando `\cover`, que recebe, em ordem:
projeto, categoria/sessão, título da obra, autor da obra, data e URL-fonte.

```text
main.tex
  ├── \cover{Formação Literária}...
  ├── sections/                        # arquivos incluídos via \input
  │   ├── 01-introducao.tex            # biografia do autor + motivação do estudo
  │   ├── 02-texto.tex                 # o poema
  │   └── 03-analise.tex               # análise crítica
  ├── fig/                             # ilustrações
  ├── ref.bib                          # bibliografia (BibLaTeX, estilo numeric)
  └── style.sty                        # estilo compartilhado
```

---

## Configuração

Um estudo é configurado inteiramente dentro de sua pasta. A estrutura geral
se segue:

- `main.tex` — ponto de entrada. Define a capa via `\cover` e inclui as seções
  com `\input`. É o arquivo que o compilador deve apontar.
- `sections/` — conteúdo dividido em arquivos numerados (`01-…`, `02-…`,
  `03-…`). O nome e a divisão variam por categoria, mas o padrão
  `NN-descricao.tex` é recomendado.
- `ref.bib` — bibliografia no formato BibLaTeX, estilo `numeric`,
  `sorting=none`.
- `fig/` — imagens e ilustrações.
- `style.sty` — estilo compartilhado que define o layout e comandos reusáveis
  (`\cover`, `\question`/`\subquestion`/`\answer`/`\demonstration`, o ambiente
  `poema` e os macros matemáticos `\NN,\ZZ,\QQ,\RR,\CC`).

### Adicionar um novo estudo

1. Crie a pasta do estudo seguindo o padrão `<categoria>/<obra>/`.
2. Copie uma estrutura existente (por exemplo,
   `comentarios-poemas/era-um-grande-passaro/`) como ponto de partida.
3. Em `main.tex`, ajuste os argumentos de `\cover`, os caminhos de `\input` e o
   arquivo de `\addbibresource`.
4. Alimente `ref.bib` com as novas fontes.
5. Compile com `latexmk` ou `./texcomp main.tex`.

---

## Licença

Este projeto está licenciado sob a **Creative Commons Attribution 4.0
International** (CC BY 4.0). Veja o arquivo [LICENSE](./LICENSE) para detalhes.
Trechos de obras e imagens históricas são incluídos para comentário crítico e
atribuídos inline.
