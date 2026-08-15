---
layout: default
title: "Jade cofà ciave SSH"
---

# Jade cofà ciave SSH

`jade-agent` el deriva la ciave privada in Jade e par ogni firma el domanda conferma; la ciave no riva mai sul computer. Completa el [setup de Jade](../jadeset/index.ve.html), aggiorna al firmware 0.1.33+ e, se te pol, dedica na Jade a le identità digitali.

```bash
sudo apt install openssh-client git python3-venv python3-dev libusb-1.0-0-dev libudev-dev
python3 -m venv ~/.local/opt/jade-agent
mkdir -p ~/.local/src && git clone https://github.com/romanz/trezor-agent.git ~/.local/src/trezor-agent
~/.local/opt/jade-agent/bin/pip install -e ~/.local/src/trezor-agent
~/.local/opt/jade-agent/bin/pip install -e ~/.local/src/trezor-agent/agents/jade
alias jade-agent="$HOME/.local/opt/jade-agent/bin/jade-agent"
jade-agent -e nist256p1 alice@vps.example.org > ~/.ssh/jade-vps.pub
jade-agent -e nist256p1 alice@vps.example.org -c
```

Mete el file publico in `authorized_keys` del server. Par GitHub registra la ciave de `git@github.com` e prima de `git push` lansa `jade-agent -e nist256p1 git@github.com --shell`. Conferma sol chele richieste previste.
