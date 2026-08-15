---
layout: default
title: "Jade comme clé SSH"
---

# Jade comme clé SSH

`jade-agent` dérive la clé privée dans Jade et demande une confirmation pour signer; elle ne va jamais sur l'ordinateur. Terminez le [setup](../jadeset/index.fr.html), mettez le firmware à jour (0.1.33+) et utilisez de préférence une Jade dédiée aux identités.

```bash
sudo apt install openssh-client git python3-venv python3-dev libusb-1.0-0-dev libudev-dev
python3 -m venv ~/.local/opt/jade-agent
mkdir -p ~/.local/src && git clone https://github.com/romanz/trezor-agent.git ~/.local/src/trezor-agent
~/.local/opt/jade-agent/bin/pip install -e ~/.local/src/trezor-agent
~/.local/opt/jade-agent/bin/pip install -e ~/.local/src/trezor-agent/agents/jade
alias jade-agent="$HOME/.local/opt/jade-agent/bin/jade-agent"
```

Exportez une clé publique par destination, ajoutez-la à `authorized_keys`, puis connectez-vous :

```bash
jade-agent -e nist256p1 alice@vps.example.org > ~/.ssh/jade-vps.pub
jade-agent -e nist256p1 alice@vps.example.org -c
```

Pour GitHub, enregistrez une clé dérivée de `git@github.com` et lancez `jade-agent -e nist256p1 git@github.com --shell` avant `git push`. Confirmez uniquement les demandes attendues.
