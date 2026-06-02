---
layout: default
name: "理解手动 Coin Control"
description: "手动 UTXO 选择的完整指南。了解它为什么重要，并学习如何在各种 software wallets（桌面端和移动端）中使用它"
title: "理解手动 Coin Control"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only 课程</span> <span>本项目由 valerio-vaccaro 维护</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

![cover](https://officinebitcoin.it/lezioni/coinco/cover.webp)

# 理解手动 Coin Control

## 引言

Bitcoin 协议的稳健性由一些简单的核心概念来保证。其中最突出的是透明性：所有 Bitcoin 交易都是公开的，任何人都可以轻松验证。虽然这一特性是协议的基石，因为它能防止欺诈并确保资金的真实性，但它也可能给保密性带来挑战。**你是否想过，如此高的透明度会不会影响你的隐私？**

你应该考虑这个问题。虽然积累 non-KYC satoshis 相当简单，但你的隐私在花费阶段最容易受到威胁。

## 当你花费一个 UTXO 时会发生什么
花费 Bitcoin 并不只是把价值转移给别人。

当你消耗自己的某个 UTXO 时，你必须满足协议透明性所要求的条件，因为你必须证明自己拥有这些资金。因此你必须：
- 暴露你的公钥；
- 生成一个数字签名。

因此，花费这一刻是最关键的：**花费 bitcoin 是一种需要有意识地、并尽可能带着控制来完成的行为**。

## Coin Control
在 Bitcoin 协议中，并不存在类似“账户”或“货币单位”的元素。UTXO 的概念不是本课的重点，但我邀请你向你信任的 Satoshi Spritz 提问，或在 Officine Bitcoin 这里申请一堂课。
你需要知道的是，在 Bitcoin 中，你积累并随后花费的是以 satoshis 计量的或小或大的会计单位，由 `unspent transaction outputs` 表示，也就是 **UTXOs**，也称为 `coins`。
当你使用 UTXOs 创建交易时，它们会被完全销毁，并在其位置创建新的 UTXOs。

Software wallets 通常会自动完成这个选择，使用“随机”选中的 coins，唯一标准是覆盖所需的花费金额。

`Coin Control`，也称为 `Coin Selection`，是某些 software wallets 的一项功能，允许你在构建交易时**手动选择要花费的 UTXOs**。

假设你有一个 wallet，里面有 3 个 UTXOs，分别为 21,000、42,000 和 63,000 satoshis。

![img](https://officinebitcoin.it/lezioni/coinco/01.webp)

如果你需要花费 24,000 sats，并让 software 自动选择，一个好的 wallet 可能会选择组合 UTXO1 + UTXO2 来支付 24k sats 和矿工费，同时创建找零，返回到原始 wallet 的一个内部地址。

![img](https://officinebitcoin.it/lezioni/coinco/02.webp)

交易之后，只计算 UTXOs，wallet 中的新情况可以概括如下。

![img](https://officinebitcoin.it/lezioni/coinco/03.webp)

然而，借助合适的 software 和你的意识，你本可以做出一个不同且更正确的选择。例如，只选择 UTXO2（42,000 sats）。

![img](https://officinebitcoin.it/lezioni/coinco/04.webp)

这样，你 wallet 中最终的 UTXO 状况会有所不同。

![img](https://officinebitcoin.it/lezioni/coinco/05.webp)

## 为什么要手动选择 UTXOs？
![img](https://officinebitcoin.it/lezioni/coinco/06.webp)

在我们的例子中，余额其实是一样的：`108,280 sats`。花费 24,000 sats 后，如果没有 coin control，wallet 中会有 2 个 UTXOs；使用手动 coin control，则总共有 3 个。

**为什么要这样做？**

我们没有使用 `UTXO1`，其中有或可能有几个原因，**这些原因也正是为什么在花费时启用手动 coin control 是一项值得遵循的良好实践**。

## 隐私
谈到手动 coin 选择时，主要优势是**花费者拥有更好的隐私**。

让我们再次使用这个例子：在_没有 coin control_ 的情况下花费 24,000 satoshis。由于 Bitcoin blockchain 是公共账本，外部观察者可以毫无疑问地判断，inputs `UTXO1 of 21,000 sats` 和 `UTXO2 of 42,000 sats`，以及找零 `UTXO5 of 38,280 sats`，**都属于同一个用户**。

相反，如果手动选择 `UTXO2`，`UTXO1` 就会保持完全私密，留在 UTXO set 中，等待在更合适的时机被花费。

`UTXO1` 可能来自 KYC 来源，例如为商品和服务收到的一笔付款，而其他 UTXOs 并非如此。

**如果这是你的 wallet，你会希望外部观察者能够如此确定地追踪到你的身份吗？** 实现手动 UTXO 选择的 wallets 允许例如**隔离一个或多个 UTXOs**，这是一项在出现这类情况时可以使用的功能。

虽然我认为 KYC 资金应当与 non-KYC bitcoin 分开存放在不同 wallet 中，但如果这正是你的情况，隔离你的一些地址会是一个根本性的帮助，而你可以通过学习手动选择花费 inputs 来做到这一点。

## 节省手续费
为一次花费选择正确的 UTXO 可以优化手续费。再次回到我们的例子，software wallet 选择了两个 UTXOs 来覆盖这笔花费。两个 UTXOs 意味着需要向网络展示两个签名，因此交易在 vBytes 上的重量更高。

使用手动 coin control，你可以只选择一个足以覆盖金额的 UTXO，从而节省手续费，因为交易“重量”降低了。

当手续费很高，但你又被迫 on-chain 花费 bitcoin（例如为了打开一个 Lightning Network 通道）时，coin control 就成为正确的经济激励。

## 找零聚合
当进行付款并使用 Bitcoin on-chain 时，收到找零的可能性几乎总会变成确定性。每一笔找零本身都是一次小的隐私损失，因为它向网络暴露了你的一个地址，而该地址可以与你原始的 input 关联起来。

考虑到最好的 HD wallets 会为找零生成专门地址，你可以轻松识别它们，并把来自不同交易的所有找零“隔离”起来；当它们达到一定金额时，你可以手动选择并合并它们，或者在 Lightning Network 上交换它们（这是我最喜欢的方法），以恢复花费过程中失去的隐私。

## 从 cold wallet 花费
Cold wallet 是一种工具，你可以借助它合理地获得较高的安全性，用来长期存放任意数量的资金。然而，意外事件可能发生，需要你动用储蓄并覆盖突发支出。

我的建议是**永远不要直接从 cold wallet 花费，以避免在同一个 wallet 的地址之间收到找零**。学习手动选择覆盖支出所需的 UTXOs，把它们转到 hot wallet，然后从那里准备你的交易。之后，任何找零都可以发送回 cold wallet 地址（如果金额合适），或用于其他目的。

## 实际演示
经过这段较长的介绍后，让我们看看如何在各种桌面端和移动端 software 中实际使用 coin control。我们将始终使用同一个 HD wallet，并将其导入每个选定工具，以展示它们之间的小差异。

## Desktop Wallets

## Sparrow
如果你使用 Sparrow，打开你的 wallet，并从左侧菜单选择 _UTXOs_。你会看到与你的 wallet 关联的所有 UTXOs 列表。

只需点击其中一个，然后选择 _Send Selected_。Sparrow 还会在命令旁边显示已选择用于花费的总额。

![img](https://officinebitcoin.it/lezioni/coinco/07.webp)

你也可以选择多个。使用 _CTRL_ 键在列表中选择不相邻的 UTXOs。

![img](https://officinebitcoin.it/lezioni/coinco/08.webp)

手动选择 UTXOs 后，Sparrow 会用图形方式清楚地展示你的交易是如何构建的，然后你可以将其最终确认并完成。

![img](https://officinebitcoin.it/lezioni/coinco/09.webp)

### UTXO 隔离
隔离资金意味着在 wallet 内“锁定”它们，使其不能作为交易 inputs 使用。

Sparrow 支持这项功能，可从 _UTXOs_ 菜单访问。将鼠标悬停在要“锁定”的 UTXO 上并右键点击。在选项中，你会找到 _Freeze_。这就是用 Sparrow Wallet 隔离一个 UTXO 的方式。

![img](https://officinebitcoin.it/lezioni/coinco/29.webp)

## Electrum
如果你的 desktop wallet 是 Electrum，你可以从 _Addresses_ 和 _Coins_ 两个菜单中手动选择 UTXOs。
在两个菜单中，选择方式都是把鼠标指向 UTXO，右键点击后选择 _Add to coin control_。

![img](https://officinebitcoin.it/lezioni/coinco/10.webp)

你也可以选择多个 UTXO，如果它们不相邻，可以使用 _CTRL_ 键。

![img](https://officinebitcoin.it/lezioni/coinco/11.webp)

Electrum 会用绿色以图形方式高亮选中的 UTXOs，底部也会有一条同色高亮栏，显示 coin control 后的可用余额。

![img](https://officinebitcoin.it/lezioni/coinco/12.webp)

一旦选择了 output(s)，你就可以像往常一样从 _Send_ 菜单构建交易。

### UTXO 隔离
Electrum 在 _Coins_ 菜单中提供这个选项：选择一个特定 UTXO，然后用鼠标右键选择 _Freeze_。你也可以从 _Addresses_ 菜单“冻结”一个没有资金的地址，或冻结该 "coin" 以阻止花费。

![img](https://officinebitcoin.it/lezioni/coinco/28.webp)

## Nunchuk
Nunchuk 打开后允许你从主菜单选择 UTXOs。
启动 Nunchuk 并点击 _View coins_。

![img](https://officinebitcoin.it/lezioni/coinco/13.webp)

随后会打开一个窗口，显示你 wallet 中的所有 UTXOs，你可以通过勾选每个金额旁边的方框来选择一个或多个。选择后，继续点击 _Create transaction_。

![img](https://officinebitcoin.it/lezioni/coinco/14.webp)

然后你可以输入目标地址，设置金额和手续费。

![img](https://officinebitcoin.it/lezioni/coinco/15.webp)

## Blockstream App
Blockstream App desktop，曾被称为 Green，允许你在开始构建交易后进行 coin 选择。打开你的 wallet 并点击 _Send_。

![img](https://officinebitcoin.it/lezioni/coinco/16.webp)

在相应字段中粘贴目标地址，然后选择 _Manual coin selection_。
![img](https://officinebitcoin.it/lezioni/coinco/17.webp)
随后会打开一个窗口，你可以在其中选择一个或多个 UTXOs。在下面的例子中，我们选择了两个 coins。然后点击 _Confirm Coin Selection_ 确认选择。

![img](https://officinebitcoin.it/lezioni/coinco/18.webp)

设置金额和手续费，然后像往常一样继续你的交易。

![img](https://officinebitcoin.it/lezioni/coinco/19.webp)

⚠️ 注意：在 Green 的 _Coins_ 菜单中，有 _Lock_/_Unlock_ 选项，暗示可以隔离 UTXOs。这只在所谓的 multisig 账户中可用；该功能只会为非常小、接近 `Dust` 阈值的 UTXOs 启用。

## Mobile Wallets

## Blue Wallet
即使在移动端，你也可以选择允许手动 UTXO 选择的 wallets。我们先看 Blue Wallet。

如果你使用这个 software，打开你的 wallet，并点击进入其中一个 wallet 的命令界面。要访问 coin control，你必须进入花费阶段，所以点击 _Send_。

![img](https://officinebitcoin.it/lezioni/coinco/21.webp)

在下一个屏幕中，选择右上角三个点所表示的菜单。会打开一个包含多个命令的下拉窗口。选择最后一个：_Coin Control_。

![img](https://officinebitcoin.it/lezioni/coinco/22.webp)

此时，Blue Wallet 会显示你的所有 UTXOs。除了金额之外，它们还用不同颜色进行图形区分。

![img](https://officinebitcoin.it/lezioni/coinco/27.webp)

选择 UTXO，然后选择 _Use Coin_。

![img](https://officinebitcoin.it/lezioni/coinco/23.webp)

Blue Wallet 会带你回到 _Send_ 窗口，以继续构建交易。调整金额和手续费，然后选择 _Next_。

![img](https://officinebitcoin.it/lezioni/coinco/24.webp)

现在你可以像往常一样完成交易。

### UTXO 隔离
Blue Wallet 也允许你隔离 UTXOs，使它们不可用于花费，这对 mobile wallet 来说是一个不错的功能。

按上文说明访问 coin control，并在选择 UTXO 后选择 _Freeze_，而不是 _Use Coin_。

![img](https://officinebitcoin.it/lezioni/coinco/26.webp)

## Nunchuk
Nunchuk 的移动版本也允许用户执行 coin control。如果你在移动端使用这个 app，打开它并进入 _Wallet_ 菜单。从这里选择 _View coins_。

![img](https://officinebitcoin.it/lezioni/coinco/30.webp)

在显示 UTXOs 列表的窗口中，点击 _Select_。

![img](https://officinebitcoin.it/lezioni/coinco/38.webp)

每个 UTXO 旁边都会出现选择功能。和 desktop 版本一样，在 Nunchuk mobile 中，手动选择是通过勾选金额旁边的方框完成的。屏幕会显示已选择的 UTXOs 数量和可用总额。完成后，左下角的 ₿ 符号就是开始构建交易的命令。

![img](https://officinebitcoin.it/lezioni/coinco/31.webp)

现在你可以完成交易，选择金额并点击 _Continue_。

![img](https://officinebitcoin.it/lezioni/coinco/32.webp)

像往常一样继续，粘贴目标地址、填写描述，并自定义手续费设置。

## Bitcoin Keeper
Bitcoin Keeper 是本指南中要看的最后一个 wallet。让我们用 single-sig wallet 看看它的 coin control 功能，尽管这种用法并不是这个特定 app 的主要目的。

在手机上设置好 Keeper 后，启动它并打开一个包含一些 UTXOs 的 wallet。在主屏幕中央，点击 _View All Coins_。

![img](https://officinebitcoin.it/lezioni/coinco/34.webp)

Keeper 会显示 UTXOs 的概览。要访问选择界面，点击 _Select To Control_。

![img](https://officinebitcoin.it/lezioni/coinco/35.webp)

你可以通过勾选 coins 并点击相应命令来选择它们。完成后，点击 _Send_。

![img](https://officinebitcoin.it/lezioni/coinco/36.webp)

Bitcoin Keeper 会直接带你进入 _Send_ 菜单，在那里你可以使用选中的 UTXOs 构建交易。

![img](https://officinebitcoin.it/lezioni/coinco/37.webp)

## Hardware wallet
本指南中看到的每一种 software wallet 都可以作为你的 hardware wallet 的 watch-only 界面。这意味着，针对离线签名设备的 coin control 也按目前看到的步骤完成。

## 一般建议
Coin control 是选择交易 inputs 的一种非常有效的实践。如果你在接收资金时已经很好地标记了 satoshis 的来源，手动选择会更加高效。如果你想掌握这项技术，我推荐这个教程：

https://planb.network/tutorials/privacy/on-chain/utxo-labelling-d997f80f-8a96-45b5-8a4e-a3e1b7788c52
