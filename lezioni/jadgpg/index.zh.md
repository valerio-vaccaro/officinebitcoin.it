---
layout: default
title: "Jade 与 GPG"
---

# Jade 与 GPG

`jade-gpg` 将签名和解密能力保留在 Jade 中，电脑只保存公钥钥匙串。完成 [设置](../jadeset/index.zh.html) 后，从源码安装组件：

```bash
sudo apt install gnupg git python3-venv python3-dev libusb-1.0-0-dev libudev-dev
python3 -m venv ~/.local/opt/jade-agent
mkdir -p ~/.local/src && git clone https://github.com/romanz/trezor-agent.git ~/.local/src/trezor-agent
~/.local/opt/jade-agent/bin/pip install -e ~/.local/src/trezor-agent
~/.local/opt/jade-agent/bin/pip install -e ~/.local/src/trezor-agent/agents/jade
export PATH="$HOME/.local/opt/jade-agent/bin:$PATH"
jade-gpg init "Alice Example <alice@example.org>"
export GNUPGHOME="$HOME/.gnupg/jade"
printf '测试\n' > message.txt
gpg --armor --detach-sign --local-user alice@example.org message.txt
gpg --verify message.txt.asc message.txt
```

在 Jade 上确认签名。保存身份、指纹和公钥，绝不要保存助记词。加密：`gpg --encrypt --recipient alice@example.org 文件`；Git 签名：`git commit -S`。
