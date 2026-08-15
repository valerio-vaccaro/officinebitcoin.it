---
layout: default
title: "Jade como clave SSH"
---

# Jade como clave SSH

## Introducción y preparación

`jade-agent` deriva la clave SSH en Jade; la privada nunca llega al ordenador y cada firma se confirma en la pantalla. `trezor-agent` es el equivalente para Trezor. Es preferible dedicar una Jade y una semilla a las identidades digitales.

Completa la [configuración de Jade](../jadeset/index.es.html), actualiza al firmware 0.1.33 o posterior, desbloquéala y conéctala por USB de datos. En Debian/Ubuntu:

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

Usa una identidad exacta por destino. Exporta la clave pública, añádela a `~/.ssh/authorized_keys` del servidor y conéctate:

```bash
jade-agent -e nist256p1 alice@vps.example.org > ~/.ssh/jade-vps.pub
jade-agent -e nist256p1 alice@vps.example.org -c
```

Para GitHub registra la salida de `jade-agent -e nist256p1 git@github.com > ~/.ssh/jade-github.pub` y abre `jade-agent -e nist256p1 git@github.com --shell` antes de `git push`. Confirma sólo solicitudes esperadas: cambiar el texto de identidad crea otra clave.
