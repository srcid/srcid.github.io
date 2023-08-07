---
layout: post
title: "Extrair dados com o jq"
categories: jq json terminal
date: 2023-08-06 23:59:00 -0300
---

Usuários de sistemas Linux, já estão habituados a usarem ferramentas de terminal que manipulam texto como o famoso editor de texto sed e outras ferramentas como o grep, awk e muitos outros. E para se trabalhar com o formato JSON temos o jq.

A ferramenta jq é um processador de linha de comando usado para manipular e transformar dados JSON. Ela permite extrair, filtrar, modificar e formatar informações contidas em estruturas JSON. Com o jq, você pode realizar consultas complexas em dados JSON, realizar transformações, realizar seleções específicas de campos e até mesmo criar scripts para automatizar tarefas de processamento de dados JSON de forma eficiente. É uma ferramenta útil para lidar com dados estruturados em formato JSON de maneira flexível e poderosa.

A seguir trago alguns exemplos de como você pode usar a ferramenta jq com a PokeAPI, que fornece informações sobre Pokémon em formato JSON.

## Extrair campo e retornar objeto JSON

Com o jq podemos extrair um campo de um objeto JSON pelo nome do campo. Então se quisermos extrair o nome de um pokemon fazemos o seguinte:

```bash
curl -s "https://pokeapi.co/api/v2/pokemon/1" | jq '.name'
```

Podemos ter o resultado em JSON, para isso basta que adicionemos chaves na _string_ de busca e o nome do campo. Ainda podemos acrescentar campos e processar seus dados.

```bash
curl -s "https://pokeapi.co/api/v2/pokemon/1" | jq '{name: .name}'
```

## Funções e condicionais

Caso se queira pegar o nome dos tipos de um pokemon em maíusculo, pode-se fazê-lo da seguinte forma usando a função `ascii_upcase`:

```bash
curl -s "https://pokeapi.co/api/v2/pokemon/1" | jq '{type1: .types[0].type.name | ascii_upcase, type2: .types[1].type.name | ascii_upcase}'
```

Porém, esse código não funcionará se `.types[1]` não existir, o que pela pokeapi pode acontecer. Tente executar o pokemon 4 e veja o que acontece.

Pare resolver esse problema a tratar o corretamente os dados, podemos usar condicionais no jq. Então o código acima ficaria assim:

```bash
curl -s "https://pokeapi.co/api/v2/pokemon/1" | jq '{type1: .types[0].type.name | ascii_upcase, type2: (if .types[1] then .types[1].type.name | ascii_upcase else null end)}
```

Desse modo, tratamos corretamente a entrada e não caimos no erro, pois a função `ascii_upcase` espera receber uma _string_.

Caso queira-se pegar os principais dados de pokemon, podemos fazê-lo desse modo:

```bash
curl -s "https://pokeapi.co/api/v2/pokemon/4" | jq '{num: .id, name: .name, hp: .stats[0].base_stat, atk: .stats[1].base_stat, def: .stats[2].base_stat, stak: .stats[3].base_stat, sdef: .stats[4].base_stat, speed: .stats[5].base_stat, type1: .types[0].type.name | ascii_upcase, type2: (if .types[1] then .types[1].type.name | ascii_upcase else null end)}'
```

Esses são alguns exemplos básicos de como usar o jq. Pretendo falar mais dele por aqui.
