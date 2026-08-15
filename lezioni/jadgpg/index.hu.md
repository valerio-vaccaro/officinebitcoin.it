---
layout: default
title: "Jade GPG-vel"
---

# Jade GPG-vel

A `jade-gpg` a Jade-en tartja az aláírási és visszafejtési képességet, a gépen csak a nyilvános kulcstartó marad. A [beállítás](../jadeset/index.hu.html) után telepítsd a forrásból:

```bash
sudo apt install gnupg git python3-venv python3-dev libusb-1.0-0-dev libudev-dev
python3 -m venv ~/.local/opt/jade-agent
mkdir -p ~/.local/src && git clone https://github.com/romanz/trezor-agent.git ~/.local/src/trezor-agent
~/.local/opt/jade-agent/bin/pip install -e ~/.local/src/trezor-agent
~/.local/opt/jade-agent/bin/pip install -e ~/.local/src/trezor-agent/agents/jade
export PATH="$HOME/.local/opt/jade-agent/bin:$PATH"
jade-gpg init "Alice Example <alice@example.org>"
export GNUPGHOME="$HOME/.gnupg/jade"
printf 'teszt\n' > message.txt
gpg --armor --detach-sign --local-user alice@example.org message.txt
gpg --verify message.txt.asc message.txt
```

Jade-en hagyd jóvá. Az identitást, ujjlenyomatot és publikus kulcsot őrizd meg, a seedet soha. Titkosítás: `gpg --encrypt --recipient alice@example.org fájl`; Git-aláírás: `git commit -S`.
