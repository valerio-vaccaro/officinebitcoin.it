---
layout: default
title: "Jade SSH-kulcsként"
---

# Jade SSH-kulcsként

A `jade-agent` a privát SSH-kulcsot a Jade-en származtatja; minden aláírást a készüléken kell jóváhagyni. Fejezd be a [Jade beállítását](../jadeset/index.hu.html), frissítsd 0.1.33+-ra, és lehetőleg külön Jade-et használj digitális identitásokhoz.

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

Tedd a nyilvános kulcsot a szerver `authorized_keys` fájljába. GitHubhoz regisztráld a `git@github.com` kulcsát és `git push` előtt indítsd: `jade-agent -e nist256p1 git@github.com --shell`. Csak várt kérést hagyj jóvá.
