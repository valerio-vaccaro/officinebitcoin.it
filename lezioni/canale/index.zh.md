---
layout: default
title: "Lightning Network non-custodial"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only 课程</span> <span>本项目由 valerio-vaccaro 维护</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

![cover](https://officinebitcoin.it/lezioni/canale/01cover.webp)

# Lightning Network non-custodial
Acinq 的 Phoenix 是一个原生 Lightning Network wallet，non-custodial，提供高效、符合 BIP39 标准、连接良好的 wallet，并把完整控制权留给用户。

你很快会发现，Phoenix 会打开一个 LN 通道，而你要对其中的余额承担 100% 的责任。
要用好 Phoenix，只需要最低限度的注意力和对 Lightning Network 的基础了解。例如，你会学会控制通道流动性，根据自己的需要保持平衡，并确保 Acinq 能看到你在线，从而让通道保持打开并维护 LN 基础设施。

# 基本操作
在[下载并验证 Phoenix apk](https://officinebitcoin.it/lezioni/verifica/index.html)之后，你可以把 app 安装到手机上。

Phoenix 打开后会询问你是要创建新 wallet，还是恢复以前的 wallet。如果这是你第一次使用 Phoenix，请选择 `Create new wallet`。随后会出现一系列欢迎界面，最后在相应位置按下 `Get started`。

![img](https://officinebitcoin.it/lezioni/canale/03.webp)

## Backup
Phoenix 打开后，**首先要做的操作一如既往是备份 wallet**。

Phoenix 采用 BIP39 标准，派生路径为 m/84'/0'/0'，会提供一组 12 个单词，你需要把它们抄写在纸上，并存放在安全的地方。

![img](https://officinebitcoin.it/lezioni/canale/04.webp)

进入菜单，让 Phoenix 向你显示 *Recovery phrase*，点击 `Display seed`。

![img](https://officinebitcoin.it/lezioni/canale/05.webp)

完成后，记得把屏幕一直滚动到底部，确认你已经完成备份，这样就不会再看到通知和警告。

![img](https://officinebitcoin.it/lezioni/canale/06.webp)

Phoenix 基本上已经可以使用。你的新 wallet 余额为零，并且可以进行配置。在左下角，你会找到再次进入设置的命令，用来配置日常使用中有用的选项。

![img](https://officinebitcoin.it/lezioni/canale/07.webp)

## 使用 Tor
从 Phoenix 的多个版本以来，Acinq 已经禁用了内置 Tor 引擎。如果你想在 Tor 保护下使用 Phoenix，需要两个步骤：
- 在 Phoenix 设置中启用 Tor
- 使用第三方 app 将 wallet 流量通过 onion 网络路由。

进入设置并选择 Tor，然后启用 `Enable Tor`，最后通过你通常使用的 app 路由流量（Orbot、Invizible Pro 等）。如果没有这些第三方 app 之一，即使在 Phoenix 设置中启用了 Tor，wallet 也无法连接到互联网。

![img](https://officinebitcoin.it/lezioni/canale/09.webp)

## 其他设置
你可以更改或设置多项功能：
- wallet 名称，点击顶部的 `Wallet` 一词；
- 从 `Display` 子菜单选择参考货币。
- 在 `Channel management` 中设置费用，这是一个重要设置，因为费用值过低可能会影响通道打开：默认设置为 5,000 sats，把它提高到 15,000；Phoenix 到时仍会使用合适的数值；
- 你应该在 `Access control` 子菜单中设置所有你认为自己能够管理的安全措施：用于花费的 PIN、用于 app 访问的 PIN 或生物识别控制；
- 在同名菜单中设置你自己的 `Electrum server`，注意 Phoenix 需要有效的 SSL 证书（例如 Let's Encrypt）；
- 启用 `Experimental features`，以申请可重复使用的 Bolt12 LN 地址
- 管理任何通道关闭，或多个 wallet 的创建/删除。

![img](https://officinebitcoin.it/lezioni/canale/08.webp)

# 打开 LN 通道 ⚡️

在 Phoenix 主屏幕上，选择 `Receive` 命令

![img](https://officinebitcoin.it/lezioni/canale/10.webp)

wallet 会提供两种接收模式，两者都有二维码：Lightning 和 Onchain。

## 支付 Lightning invoice

![img](https://officinebitcoin.it/lezioni/canale/11.webp)

打开 LN 通道的一种快速方法，是用 Phoenix 创建一张 invoice，并用另一个 LN wallet 支付它。

第一笔入账付款会决定通道的打开，通道的流动性由你刚刚创建的 invoice 金额决定（不包括打开通道的 onchain 交易费用）。

尽管会显示一个临时等待 onchain 确认的提示，资金也可能立即可用。或者你可能需要等待才能使用它们。

## Onchain 交易
打开 LN 通道始终是一笔 onchain 交易，2-of-2 multisig：你和对手方（Acinq）用你的资金建立条件。

如果你无法支付或接收 Lightning invoice，但你有 onchain 资金，可以使用 Phoenix 为你显示的 onchain 地址。

交易之后，Phoenix 看起来是这样：

![img](https://officinebitcoin.it/lezioni/canale/12.webp)

app 会提醒你，需要等待 3 个 blockchain 确认，才能使用资金。

# 管理通道流动性
一旦收到 3 个确认，你的 LN wallet 就可以使用了。

起初它的所有流动性都是出站的，你只能花费；你可以在 `Settings -> Advanced -> Payment Channels` 中看到这一点

![img](https://officinebitcoin.it/lezioni/canale/13.webp)

你可以通过支付一张或多张 Lightning Network invoice 来创建入站流动性。

# 使用 wallet

使用 Phoenix wallet 是一种愉快且非常简单的体验。

唯一需要记住的是：
1. 你刚刚创建的通道，是你和 Acinq 之间的一个 smart contract，由你的资金提供支持；
2. 通道状态备份和基础设施维护的繁重工作由 Acinq 处理，它会针对你执行的付款操作向你收取少量额外 sat 作为费用；
3. 定期访问你的 wallet，打开它并不时进行操作，因为如果对手方注意到你长期缺席并认为你是 "zombie"，它可能决定关闭通道。Acinq 关闭通道，是为了避免花费资源和时间维护备份及休眠通道；
4. 如果你不再需要使用这个通道，也可以决定关闭它。
5. 在通道关闭的情况下，`cooperative closure` 流程是最佳选择，因为它能避免许多问题。

## Splicing
这里要特别提到 `Splicing` 技术，它由 Acinq 实现，可以增加或减少通道总容量。

Splicing 很有意思：如果你有一个容量为 `tot` 的通道，就可以扩展或缩减它。看起来这些操作似乎取决于每个人的需要，**但事情没有这么简单**。

你必须始终记住，**Phoenix 是一个 Lightning Network wallet**，即使它支持 Bitcoin 的 Layer1，也应该用于 Layer2 上的小额支付。

**事实上，每一次 onchain 操作都会被 Acinq 理解为修改通道容量的理由**：
- 从 onchain wallet 向 Phoenix 接收 `xsats` 金额：Acinq 会扩展通道，把容量从 `tot` 提高到 `tot + xsats`
- 从 Phoenix 向 onchain 地址支付 `ysats` 金额：Acinq 会缩减通道，把容量从 `tot` 降低到 `tot - ysats`。

`Splicing` 是一笔 onchain 交易（2-of-2 multisig），会产生费用。虽然费用低于通道打开/关闭，但草率地或在错误时机进行这些操作，可能导致不必要的高成本。

要在 LN 和 Onchain 之间来回移动资金，尽量使用合适的 `swap` 工具，不要为此使用 Phoenix Wallet。

# 恢复资金
最后，也是最重要的一点，拥有 **non-custodial** 工具的重要性就在这里体现出来。

如果以及当通道关闭时，你可以**把 12 个备份单词导入支持 BIP39 标准的 wallet，从而恢复你的 onchain 资金**。

在其他选择中，Electrum wallet 是一种让这个操作简单直观的选择。

如果 wallet 反而是 *custodial*，而你并不拥有密钥，你可能会遇到各种问题，从难以与一个*没有人情味的客服*互动，到为了取回资金而接受繁重的 `kyc`，**一直到无法恢复你的资金（无论总金额是多少）**。

值得吗？

# 学习支持
如果你参加了 Telegram 上的现场演示，可以把它视为迈向个人主权（不只是金融主权）的又一步。
如果你错过了，**不要绝望**：这些笔记正是为了帮助你补上内容，而且你也应该知道，我们会在 Officine 再次举办。

为了不错过下一次演示，请加入 [Telegram 群组](https://t.me/officinebitcoin)，以便持续获得更新。

![img](https://officinebitcoin.it/lezioni/canale/14.webp)

你还可以找到离你最近的 [Satoshi Spritz](https://satoshispritz.it/)。Satoshi Spritz 是一个本地 meetup，只讨论 Bitcoin，你可以带着问题前来，并从其他有经验的 bitcoiners 那里获得回答。在链接中你会找到半岛地图。

![img](https://officinebitcoin.it/lezioni/canale/15.webp)

最后，如果你附近没有 meetup，可以参加 [SatoshiSpritz Connect](https://t.me/SatoshiSpritzConnect) 每周直播，这是一个虚拟 meetup，专为无法参加 Satoshi Spritz 的人创建，也用于帮助较小的 meetup 记录笔记，并为他们自己的演示寻找灵感。

![img](https://officinebitcoin.it/lezioni/canale/16.webp)
