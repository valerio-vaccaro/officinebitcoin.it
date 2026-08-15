---
layout: default
title: "Jade come ciav SSH"
---

# Jade come ciav SSH

`jade-agent` el deriva la ciav privada dent in Jade e per ogni firma el domanda conferma; la ciav la va mai sul computer. Completa el [setup de Jade](../jadeset/index.mi.html), aggiorna al firmware 0.1.33+ e, se te pò, dedica una Jade a le identità digital.

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

Mett el file pubblic in `authorized_keys` del server. Per GitHub registra la ciav de `git@github.com` e prima de `git push` lancia `jade-agent -e nist256p1 git@github.com --shell`. Conferma domà i domand previst.
