---
layout: post
title: "Tutorial do comando update-alternatives"
categories: linux comando terminal
date: 2022-03-22 14:16:28 -0300
---

O comando update-alternatives existe na maioria das distribuições linux e é muito útil para gerenciar
versões ou simplesmente alterar o nome de certos executáveis.

## Comando fd

O comando fd é uma alternativa ao comando find que no Debian e derivados teve o nome do executável alterado
para fdfind. Isso não me agrada e gostaria de alterá-lo.

## Solução

sudo update-alternatives --install '/usr/local/bin/fd' 'fd' "$(which fdfind)" 100
