---
layout: default
title: "Jade como chave SSH"
---

# Jade como chave SSH

## Introdução e preparação

`jade-agent` deriva a chave SSH na Jade; a chave privada nunca chega ao computador e cada assinatura é confirmada no ecrã. `trezor-agent` é o equivalente para Trezor. É mais prudente dedicar uma Jade e seed às identidades digitais.

Conclua o [setup da Jade](../jadeset/index.pt.html), atualize para firmware 0.1.33+, desbloqueie e ligue por USB de dados:

```bash
sudo apt update
sudo apt install openssh-client git python3-venv python3-dev libusb-1.0-0-dev libudev-dev
python3 -m venv ~/.local/opt/jade-agent
mkdir -p ~/.local/src
git clone https://github.com/romanz/trezor-agent.git ~/.local/src/trezor-agent
~/.local/opt/jade-agent/bin/pip install -e ~/.local/src/trezor-agent
~/.local/opt/jade-agent/bin/pip install -e ~/.local/src/trezor-agent/agents/jade
alias jade-agent="$HOME/.local/opt/jade-agent/bin/jade-agent"
```

## Uso

Use uma identidade exata por destino, exporte a chave pública, adicione-a ao `~/.ssh/authorized_keys` do servidor e ligue-se:

```bash
jade-agent -e nist256p1 alice@vps.example.org > ~/.ssh/jade-vps.pub
jade-agent -e nist256p1 alice@vps.example.org -c
```

Para GitHub, registe `jade-agent -e nist256p1 git@github.com > ~/.ssh/jade-github.pub` e abra `jade-agent -e nist256p1 git@github.com --shell` antes de `git push`. Confirme apenas pedidos esperados; texto de identidade diferente cria outra chave.
