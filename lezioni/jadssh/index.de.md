---
layout: default
title: "Jade als SSH-Schlüssel"
---

# Jade als SSH-Schlüssel

`jade-agent` leitet den privaten Schlüssel auf Jade ab und verlangt jede Signaturbestätigung; der Schlüssel erreicht den Computer nie. Führen Sie das [Jade-Setup](../jadeset/index.de.html) durch, aktualisieren Sie auf Firmware 0.1.33+ und verwenden Sie möglichst eine eigene Jade für Identitäten.

```bash
sudo apt install openssh-client git python3-venv python3-dev libusb-1.0-0-dev libudev-dev
python3 -m venv ~/.local/opt/jade-agent
mkdir -p ~/.local/src && git clone https://github.com/romanz/trezor-agent.git ~/.local/src/trezor-agent
~/.local/opt/jade-agent/bin/pip install -e ~/.local/src/trezor-agent
~/.local/opt/jade-agent/bin/pip install -e ~/.local/src/trezor-agent/agents/jade
alias jade-agent="$HOME/.local/opt/jade-agent/bin/jade-agent"
```

```bash
jade-agent -e nist256p1 alice@vps.example.org > ~/.ssh/jade-vps.pub
jade-agent -e nist256p1 alice@vps.example.org -c
```

Fügen Sie die öffentliche Schlüsseldatei auf dem Server zu `authorized_keys` hinzu. Für GitHub registrieren Sie die aus `git@github.com` abgeleitete Schlüsseldatei und starten vor `git push` `jade-agent -e nist256p1 git@github.com --shell`. Nur erwartete Anfragen bestätigen.
