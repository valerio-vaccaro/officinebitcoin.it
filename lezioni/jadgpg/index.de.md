---
layout: default
title: "Jade mit GPG"
---

# Jade mit GPG

`jade-gpg` belässt Signieren und Entschlüsseln auf Jade; GnuPG hält nur den öffentlichen Schlüsselbund. Nach dem [Setup](../jadeset/index.de.html):

```bash
sudo apt install gnupg git python3-venv python3-dev libusb-1.0-0-dev libudev-dev
python3 -m venv ~/.local/opt/jade-agent
mkdir -p ~/.local/src && git clone https://github.com/romanz/trezor-agent.git ~/.local/src/trezor-agent
~/.local/opt/jade-agent/bin/pip install -e ~/.local/src/trezor-agent
~/.local/opt/jade-agent/bin/pip install -e ~/.local/src/trezor-agent/agents/jade
export PATH="$HOME/.local/opt/jade-agent/bin:$PATH"
jade-gpg init "Alice Example <alice@example.org>"
export GNUPGHOME="$HOME/.gnupg/jade"
```

```bash
printf 'Test\n' > nachricht.txt
gpg --armor --detach-sign --local-user alice@example.org nachricht.txt
gpg --verify nachricht.txt.asc nachricht.txt
```

Bestätigen Sie auf Jade; sichern Sie Identität, Fingerabdruck und öffentlichen Schlüssel, niemals die Seed. Verschlüsseln: `gpg --encrypt --recipient alice@example.org datei`; Git signieren: `git commit -S`.
