---
layout: default
title: "将 Jade 用作 SSH 密钥"
---

# 将 Jade 用作 SSH 密钥

`jade-agent` 在 Jade 内派生 SSH 私钥，并要求在设备屏幕上确认每次签名；私钥永远不会到达电脑。完成 [Jade 设置](../jadeset/index.zh.html)，升级至 0.1.33 或更新固件，并最好为数字身份使用独立的 Jade 和助记词。

```bash
sudo apt install openssh-client git python3-venv python3-dev libusb-1.0-0-dev libudev-dev
python3 -m venv ~/.local/opt/jade-agent
mkdir -p ~/.local/src && git clone https://github.com/romanz/trezor-agent.git ~/.local/src/trezor-agent
~/.local/opt/jade-agent/bin/pip install -e ~/.local/src/trezor-agent
~/.local/opt/jade-agent/bin/pip install -e ~/.local/src/trezor-agent/agents/jade
alias jade-agent="$HOME/.local/opt/jade-agent/bin/jade-agent"
jade-agent -e nist256p1 alice@vps.example.org > ~/.ssh/jade-vps.pub
jade-agent -e nist256p1 alice@vps.example.org -c
```

将公钥加入服务器的 `authorized_keys`。GitHub 使用为 `git@github.com` 导出的公钥，并在 `git push` 前执行 `jade-agent -e nist256p1 git@github.com --shell`。只确认自己预期的请求。
