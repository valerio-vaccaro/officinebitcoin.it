---
layout: default
title: "Jade con GPG"
---

# Jade con GPG

## Introducción y preparación

`jade-gpg` deja la capacidad de firmar y descifrar en Jade, mientras GnuPG mantiene el llavero público en el ordenador. No uses para una identidad pública una semilla bitcoin de valor; una Jade dedicada es más segura.

Completa el [setup de Jade](../jadeset/index.es.html), actualiza el firmware y ejecuta:

```bash
sudo apt update
sudo apt install gnupg git python3-venv python3-dev libusb-1.0-0-dev libudev-dev
python3 -m venv ~/.local/opt/jade-agent
mkdir -p ~/.local/src
git clone https://github.com/romanz/trezor-agent.git ~/.local/src/trezor-agent
~/.local/opt/jade-agent/bin/pip install -e ~/.local/src/trezor-agent
~/.local/opt/jade-agent/bin/pip install -e ~/.local/src/trezor-agent/agents/jade
export PATH="$HOME/.local/opt/jade-agent/bin:$PATH"
```

## Crear y usar la identidad

```bash
jade-gpg init "Alice Example <alice@example.org>"
export GNUPGHOME="$HOME/.gnupg/jade"
gpg --armor --export alice@example.org > alice-public.asc
printf 'prueba\n' > mensaje.txt
gpg --armor --detach-sign --local-user alice@example.org mensaje.txt
gpg --verify mensaje.txt.asc mensaje.txt
```

Jade debe confirmar la firma. Conserva identidad, huella y clave pública, nunca la semilla. Para cifrar: `gpg --encrypt --recipient alice@example.org archivo`; para Git: `git commit -S`.
