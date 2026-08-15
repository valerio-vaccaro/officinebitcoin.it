---
layout: default
title: "Jade with GPG"
---

# Jade with GPG

## Introduction

`jade-gpg` lets Jade hold the signing/decryption capability while GnuPG on the computer keeps the public keyring. Do not use a bitcoin seed of material value for a public digital identity; a dedicated Jade is safer.

## Set up Jade and the computer

Complete [Jade setup](../jadeset/index.en.html), update to firmware 0.1.33 or newer, then install the Jade component from source:

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

## Create and use the identity

Keep this hardware keyring separate from ordinary software keys:

```bash
jade-gpg init "Alice Example <alice@example.org>"
export GNUPGHOME="$HOME/.gnupg/jade"
gpg --armor --export alice@example.org > alice-public.asc
printf 'test\n' > message.txt
gpg --armor --detach-sign --local-user alice@example.org message.txt
gpg --verify message.txt.asc message.txt
```

Jade must confirm signing. Record the exact identity, fingerprint and public key; never record the seed on the computer. Use `gpg --encrypt --recipient alice@example.org file` to encrypt for yourself, and `git commit -S` to sign a Git commit.
