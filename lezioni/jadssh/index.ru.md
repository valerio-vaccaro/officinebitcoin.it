---
layout: default
title: "Jade как ключ SSH"
---

# Jade как ключ SSH

`jade-agent` выводит приватный SSH-ключ внутри Jade и запрашивает подтверждение подписи; ключ не попадает на компьютер. Завершите [настройку Jade](../jadeset/index.ru.html), обновите прошивку до 0.1.33+ и по возможности выделите отдельную Jade для идентичностей.

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

Добавьте публичный ключ на сервер в `authorized_keys`. Для GitHub зарегистрируйте ключ для `git@github.com`, затем перед `git push` запустите `jade-agent -e nist256p1 git@github.com --shell`. Подтверждайте только ожидаемые запросы.
