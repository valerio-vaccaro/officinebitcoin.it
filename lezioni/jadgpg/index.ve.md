---
layout: default
title: "Jade co GPG"
---

# Jade co GPG

`jade-gpg` el tien in Jade la capacità de firmar e decifrar; sul computer ghe xe sol el portaciave publico. Dopo el [setup](../jadeset/index.ve.html):

```bash
sudo apt install gnupg git python3-venv python3-dev libusb-1.0-0-dev libudev-dev
python3 -m venv ~/.local/opt/jade-agent
mkdir -p ~/.local/src && git clone https://github.com/romanz/trezor-agent.git ~/.local/src/trezor-agent
~/.local/opt/jade-agent/bin/pip install -e ~/.local/src/trezor-agent
~/.local/opt/jade-agent/bin/pip install -e ~/.local/src/trezor-agent/agents/jade
export PATH="$HOME/.local/opt/jade-agent/bin:$PATH"
jade-gpg init "Alice Example <alice@example.org>"
export GNUPGHOME="$HOME/.gnupg/jade"
printf 'prova\n' > message.txt
gpg --armor --detach-sign --local-user alice@example.org message.txt
gpg --verify message.txt.asc message.txt
```

Conferma su Jade. Tegni identità, impronta e ciave publica, mai la seed. Sifra co `gpg --encrypt --recipient alice@example.org file`; firma Git co `git commit -S`.
