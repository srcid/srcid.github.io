---
layout: post
date: 2022-03-26 12:16:53 -0300
categories: pdf terminal
title: "Mergear PDFs no terminal"
---

É comum lidarmos com arquivos PDF e é comum que precisemos _mergeá-los_ ou uni-los em um só arquivo. Em sistemas operacionais linux temos as ferramentas do projeto popple que podem ser instaladas como informado a baixo em sistemas base debian.

```
sudo apt install popple-utils
```

Esse pacote nos dá varias ferramentas para trabalharmos com PDFs

- pdfdetach -- lists or extracts embedded files (attachments)
- pdffonts -- font analyzer
- pdfimages -- image extractor
- pdfinfo -- document information
- pdfseparate -- page extraction tool
- pdfsig -- verifies digital signatures
- pdftocairo -- PDF to PNG/JPEG/PDF/PS/EPS/SVG converter using Cairo
- pdftohtml -- PDF to HTML converter
- pdftoppm -- PDF to PPM/PNG/JPEG image converter
- pdftops -- PDF to PostScript (PS) converter
- pdftotext -- text extraction
- pdfunite -- document merging tool

## Como usar pdfunite

```
pdfunite f1.pdf f2.pdf ... fn.pdf fout.pdf
```

Porém, o __pdfunite__ não entrelaça, apenas liga o final com o começo dos arquivos passados como parâmentro 
na ordem no qual foram dados

## Ferramenta pdftk

O __pdftk__ é outra ferramente para trabalhar com PDFs que nos permite entrelaçar PDFs. Ele faz muito mas do 
que isso, porém o escopo desse texto é apenas _merge_. Podemos instalá-lo desse modo.

```
sudo snap install pdftk
```

Para entrelaçar arquivos, use o seguinte comando.

```
pdftk A=f1.pdf B=f2.pdf shuffle A B output f1_f2_interlaced.pdf
```

