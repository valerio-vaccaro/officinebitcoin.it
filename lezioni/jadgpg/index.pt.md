---
layout: default
title: "Jade com GPG"
---

# Jade com GPG

## Introdução e preparação

`jade-gpg` mantém a capacidade de assinar/desencriptar na Jade e o chaveiro público no computador. Não use uma seed bitcoin valiosa para uma identidade pública; uma Jade dedicada é mais segura.

Conclua o [setup](../jadeset/index.pt.html) e instale o componente Jade da fonte:

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

## Criar e usar

```bash
jade-gpg init "Alice Example <alice@example.org>"
export GNUPGHOME="$HOME/.gnupg/jade"
printf 'teste\n' > mensagem.txt
gpg --armor --detach-sign --local-user alice@example.org mensagem.txt
gpg --verify mensagem.txt.asc mensagem.txt
```

Confirme a assinatura na Jade. Guarde identidade, impressão digital e chave pública, nunca a seed. Use `gpg --encrypt --recipient alice@example.org ficheiro` para cifrar e `git commit -S` para Git.
