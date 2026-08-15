---
layout: default
title: "Jade avec GPG"
---

# Jade avec GPG

`jade-gpg` garde la capacité de signer et déchiffrer dans Jade; GnuPG ne conserve que le trousseau public. Après le [setup](../jadeset/index.fr.html), installez l'agent source :

```bash
sudo apt install gnupg git python3-venv python3-dev libusb-1.0-0-dev libudev-dev
python3 -m venv ~/.local/opt/jade-agent
mkdir -p ~/.local/src && git clone https://github.com/romanz/trezor-agent.git ~/.local/src/trezor-agent
~/.local/opt/jade-agent/bin/pip install -e ~/.local/src/trezor-agent
~/.local/opt/jade-agent/bin/pip install -e ~/.local/src/trezor-agent/agents/jade
export PATH="$HOME/.local/opt/jade-agent/bin:$PATH"
```

```bash
jade-gpg init "Alice Example <alice@example.org>"
export GNUPGHOME="$HOME/.gnupg/jade"
printf 'test\n' > message.txt
gpg --armor --detach-sign --local-user alice@example.org message.txt
gpg --verify message.txt.asc message.txt
```

Confirmez la signature sur Jade. Gardez identité, empreinte et clé publique, jamais la seed. Chiffrez avec `gpg --encrypt --recipient alice@example.org fichier` et signez Git avec `git commit -S`.
