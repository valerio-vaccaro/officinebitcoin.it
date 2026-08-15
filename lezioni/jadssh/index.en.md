---
layout: default
title: "Jade as an SSH key"
---

# Jade as an SSH key

## Introduction

`jade-agent` derives an SSH key on Jade and asks for confirmation before each signature; the private key never reaches the computer. `trezor-agent` is the equivalent command for a Trezor, while Jade uses `jade-agent`. Prefer a Jade and seed dedicated to digital identities, not bitcoin savings.

## Set up Jade and the computer

Finish [Jade setup](../jadeset/index.en.html), update firmware (0.1.33 or later), unlock Jade and connect it with a data USB cable. On Debian/Ubuntu:

```bash
sudo apt update
sudo apt install openssh-client git python3-venv python3-dev libusb-1.0-0-dev libudev-dev
python3 -m venv ~/.local/opt/jade-agent
mkdir -p ~/.local/src
git clone https://github.com/romanz/trezor-agent.git ~/.local/src/trezor-agent
~/.local/opt/jade-agent/bin/pip install -e ~/.local/src/trezor-agent
~/.local/opt/jade-agent/bin/pip install -e ~/.local/src/trezor-agent/agents/jade
alias jade-agent="$HOME/.local/opt/jade-agent/bin/jade-agent"
```

`jade-agent` is installed from source, not PyPI. If Jade is not detected, check the data cable and [udev rules](https://github.com/bitcoin-core/HWI/blob/master/hwilib/udev/55-usb-jade.rules).

## Use it

Use one exact, non-secret identity per destination. Export its public key, add it to the server's `~/.ssh/authorized_keys`, then connect:

```bash
jade-agent -e nist256p1 alice@vps.example.org > ~/.ssh/jade-vps.pub
jade-agent -e nist256p1 alice@vps.example.org -c
```

For GitHub, register `jade-agent -e nist256p1 git@github.com > ~/.ssh/jade-github.pub` as an SSH key, then run `jade-agent -e nist256p1 git@github.com --shell` before `git push`. Confirm only expected requests on Jade; changing the identity text creates a different key.
