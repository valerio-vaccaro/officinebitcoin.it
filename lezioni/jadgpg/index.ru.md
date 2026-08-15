---
layout: default
title: "Jade с GPG"
---

# Jade с GPG

`jade-gpg` оставляет возможность подписи и расшифрования в Jade, а GnuPG хранит публичный брелок. После [настройки](../jadeset/index.ru.html):

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
printf 'тест\n' > message.txt
gpg --armor --detach-sign --local-user alice@example.org message.txt
gpg --verify message.txt.asc message.txt
```

Подтвердите подпись на Jade. Храните идентичность, отпечаток и публичный ключ, но никогда seed. Шифрование: `gpg --encrypt --recipient alice@example.org файл`; подпись Git: `git commit -S`.
