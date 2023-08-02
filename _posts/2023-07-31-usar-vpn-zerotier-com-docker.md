---
layout: post
title: "Usar VPN zerotier com Docker"
categories: vpn docker linux zerotier
date: 2023-07-31 20:58:00 -0300
---

A zerotier é um serviço de VPN, similar ao hamachi, muito usado para servidores de minecraft. Uma forma simples de nos conectarmos a uma rede da zerotir é usando o container disponibilizado pela própria empresa, que facilita muito a instalação.

## Verificar dispositivo tun

Execute o comando abaixo, se o arquivo `/dev/net/tun` não existir é necessario carregá-lo.

```bash
ls /dev/net/tun
```

## Executar container

Com o comando abaixo estamos executando o container da zerotier. Caso queira que o container seja executado no boot, adicione o parâmetro `--restart=always` ou `--restart=unless-stopped`. 

```bash
docker run -d --name zt --network host --cap-add SYS_ADMIN --cap-add NET_ADMIN --device /dev/net/tun zerotier/zerotier:latest <id da rede>
```

## Verificar a conexão

É possível verificar a conexão usando o comando `docker exec zt zerotier-cli status` ou na interface web da própria zerotier.