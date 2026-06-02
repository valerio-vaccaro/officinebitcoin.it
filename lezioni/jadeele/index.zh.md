---
layout: default
title: "Jade 与 Electrum Wallet"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only 课程</span> <span>本项目由 valerio-vaccaro 维护</span></p>

## 🌍 翻译

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Jade 与 Electrum Wallet

![alt text](https://officinebitcoin.it/lezioni/jadeele/0_cover.jpg)

Jade 初始化之后，就可以开始使用它；为此，需要选择一个用于查看的钱包。

Jade 是一种设备，可以与多个钱包配合使用，也可以与 Blockstream 在其网站上所称的 companion apps 配合使用。

本教程将介绍通过 USB 与 Electrum Wallet 一起使用的各个步骤。

拿起已经初始化的 Jade。刚开机时，它会显示如下：


![alt text](https://officinebitcoin.it/lezioni/jadeele/001.jpg)

选择 Unlock Jade 后，会出现一个菜单，需要在其中选择如何将设备连接到 companion app。

使用 Electrum 时，Jade 只能通过 USB 连接，因此应选择该方式。

启动 Electrum，它会打开，并默认建议打开上一次使用的钱包。

如果这是第一次将 Jade 连接到 Electrum，请选择 Create New Wallet，然后选择 Finish。

![alt text](https://officinebitcoin.it/lezioni/jadeele/1.jpg)

给钱包命名，例如 Jade_Officine。

![alt text](https://officinebitcoin.it/lezioni/jadeele/3.jpg)

选择 Standard Wallet

![alt text](https://officinebitcoin.it/lezioni/jadeele/4.jpg)

在选择 keystore 时，务必选择 Use a hardware device。

![alt text](https://officinebitcoin.it/lezioni/jadeele/5.jpg)

Electrum 开始扫描以查找 hardware 设备

![alt text](https://officinebitcoin.it/lezioni/jadeele/6.jpg)

将 USB 连接到电脑后（USB C 一端已经连接到 Jade），hardware wallet 会显示锁定界面。输入 setup 期间设置的六位 PIN，即可解锁 Jade


![alt text](https://officinebitcoin.it/lezioni/jadeele/7.jpg)

hardware 设备解锁后，Electrum 会检测到 Jade。点击 Next 继续。

![alt text](https://officinebitcoin.it/lezioni/jadeele/8.jpg)

此时 Electrum 会要求设置 script policy；请选择 Native Segwit。

![alt text](https://officinebitcoin.it/lezioni/jadeele/9.jpg)

随后开始将 Jade 上钱包的公钥传输到 Electrum 查看钱包。

![alt text](https://officinebitcoin.it/lezioni/jadeele/10.jpg)

公钥导出完成后，流程就结束了。

watch-only 钱包已准备就绪，Electrum 会通过下面的界面提示完成。

![alt text](https://officinebitcoin.it/lezioni/jadeele/11.jpg)

钱包确实已经创建，可以开始查看它：可以看到 addresses、wallet information，尤其是在右下角可以看到提示，表明这是由 Blockstream Jade 创建的钱包。Blockstream 标志旁边的绿色圆点表示设备已开机并正确连接。

![alt text](https://officinebitcoin.it/lezioni/jadeele/12.jpg)

接收和支出交易

在 Electrum 的 Receive 菜单中，生成一个用于接收资金的 scriptPubKey（地址）。始终从小额开始，并进行一次接收+支出测试。

![alt text](https://officinebitcoin.it/lezioni/jadeele/13.jpg)

收到 sats 后，可以在 History 菜单中检查到账情况。

![alt text](https://officinebitcoin.it/lezioni/jadeele/14.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeele/15.jpg)

交易确认后，就可以花费这个 UTXO 并结束测试。

支出将需要使用 Jade 进行签名。

进入 Electrum 的 Send 菜单，粘贴一个 scriptPubKey，并仔细检查。

![alt text](https://officinebitcoin.it/lezioni/jadeele/16.jpg)

完成后，按 Pay。

交易窗口会打开，在这里设置正确的交易 fees 很重要。完成所有设置后，点击右下角的 Preview。

![alt text](https://officinebitcoin.it/lezioni/jadeele/17.jpg)

交易窗口会显示一些重要细节，首先是 status: Unsigned。

在这个阶段还可以看到 Sign 命令，用于通过 Jade 添加签名。

![alt text](https://officinebitcoin.it/lezioni/jadeele/18.jpg)

Electrum 会提示按照 hardware 设备上的说明操作，此时设备已准备好签名。

不过，在签名前最好先核对要签名的内容：刚刚设置的交易所有参数也会显示在 Jade 上，并且都可以逐一核对。

![alt text](https://officinebitcoin.it/lezioni/jadeele/19.jpg)

要继续，请确保光标始终停在通向下一步的箭头 → 上，而不要停在会取消操作的 "X" 上。

当 Jade 显示 fees 时，核对显示结束。此时确认就等同于添加签名。

![alt text](https://officinebitcoin.it/lezioni/jadeele/20.jpg)

Jade 会短暂处理签名。

![alt text](https://officinebitcoin.it/lezioni/jadeele/21.jpg)

与此同时，在 Electrum 中可以看到交易的 status 已从 Unsigned 变为 Signed，现在可以点击 Broadcast 来传播交易。

![alt text](https://officinebitcoin.it/lezioni/jadeele/22.jpg)

经过这样测试的钱包，可以用于接收打算安全保存的 UTXO。

![alt text](https://officinebitcoin.it/lezioni/jadeele/23.jpg)
