---
layout: default
name: "Bitcoin 入门套件"
description: "一个简单且易于实施的入门套件，用于正确使用 Bitcoin。学习如何下载并安装移动 wallet、配置用于付款请求的 POS，并了解 wallet 的高级设置。"
title: "初始术语表"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only 课程</span> <span>此项目由 valerio-vaccaro 维护</span></p>

## 🌍 翻译

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

![cover](assets/cover.webp)

这是开始以尽可能正确的方式使用 Bitcoin 的好方法。下面是一套非常轻量、易于实施的 *starter kit* 建议，你可以独立完成配置。

无论你是好奇的用户、希望把 Bitcoin 作为支付方式的专业人士，还是想为朋友和家人寻找方案的资深用户，本指南都将帮助你：
- 下载并安装一个移动 wallet，用于各个层级的 Bitcoin 使用（onchain 用于长期保存；Liquid 和 Lightning 用于即时支付）；
- 配置一个 POS，根据你的商品/服务的欧元价格生成付款请求；
- 了解 wallet 的高级设置。我们把这一部分放在指南末尾，是为了简化初次上手，但请务必阅读，因为它很重要。

先说明一下，当我们说以 *正确方式* 使用 Bitcoin 时，具体是什么意思。

# 初始术语表
- `Not your keys, not your coins`
  如果你第一次接触 Bitcoin，`Not your keys, not your coins` 这句话对你来说可能很陌生，含义也许只停留在字面翻译。Bitcoin 基于非对称密码学原理运行，依赖一组组公钥和私钥。只有**唯一**持有并自行管理私钥，你才能说自己控制着你的 Bitcoin。
  
  因此，只有你自己应该知道私钥；这些私钥是让你拥有并最终花费与其关联的 bitcoin 的秘密。`Not your keys, not your coins` 几乎是全世界 bitcoiners 的 _mantra_，也会成为你的原则。

- `Recovery phrase`
  在短暂的发展历史中，Bitcoin 协议不断演进，让秘密也就是私钥的管理更简单。如今它们以 12 或 24 个英文单词的序列表示，更便于抄写和校验。这些单词是需要保管的主要秘密。必须抄写在纸上，并放在非常安全的地方，例如保险箱。绝不能拍照、传到电脑上，更不能与他人分享。

- `Wallet`
  Wallet 是让你查看余额、接收或花费 Bitcoin 的工具。本教程中，我们会在你的手机上下载一个 wallet。手机上的 wallet 称为 `hot wallet`，因为它位于始终连接互联网的设备上。对于刚开始的人来说，这完全可以；随着学习，你会了解其他方法来完善 wallet 的使用。

- `Non Custodial`
  从 `non-custodial` wallet 开始使用 Bitcoin 非常重要，也就是使用那些**让你完全控制私钥**的钱包。对于任何推动你使用其他所谓 custodial 工具来接触 Bitcoin 的人，都要保持谨慎。Custodial wallet 是你不拥有其密钥的工具。问题不是**会不会**，而是**什么时候**它们会永久阻止你访问资金。

# Blockstream App (ex Green Wallet)
在 starter kit 中，我们将下载 Blockstream App，这是一个 `open source` wallet，你可以检查它的代码。该应用有长期的开发传统和不错的历史；这个 wallet 过去已经证明可靠。

---
⚠️ 以下说明用于在 Android 上下载并安装 app。iOS 必须使用官方商店。

---

## 🌍 翻译

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

打开链接 https://github.com/Blockstream/green_android，这是开发者的官方 Github 仓库。

![img](assets/01.webp)

在页面中部右侧的 *Releases* 区域选择 `Latest`，以下载最新版本。

你会进入显示最新 release 的页面；在撰写本教程的 2025 年 12 月，最新版本为 5.1.4。在同一页面选择可下载的内容：

![img](assets/02.webp)

下载 `.apk` 文件，无需经过 Play Store，然后安装到你的 Android 手机上。

![img](assets/03.webp)

---
⚠️ 你的手机可能会要求特殊权限，才能从未认证来源下载 app。授予这些权限以继续。

---
当 Android 要求安装 Blockstream App 时，点击 `Install`。

![img](assets/04.webp)

安装结束后，选择 `Open`。

![img](assets/05.webp)

Blockstream App 打开后，为开始使用 wallet，选择 `Get Started`。

![img](assets/07.webp)

Blockstream 会询问你是否愿意参与数据收集，以帮助开发者改进 app。请拒绝邀请。

![img](assets/08.webp)

# 你的第一个 wallet
你可以开始创建第一个 wallet。点击 `Set Up Mobile Wallet`。

![img](assets/09.webp)

Wallet 创建流程开始。

![img](assets/10.webp)

几秒钟后完成。你的 wallet 已准备好；要开始使用，请点击 `Continue`。

![img](assets/11.webp)

Wallet 会在名为 `Home` 的屏幕中打开。现在可以先看一下，但应立即关注底部菜单 `Security`。

# 你的密钥，你的币

![img](assets/12.webp)

在此菜单中，系统会提示你备份 wallet。这只是显示一串 12 个单词，你将来需要用它们恢复 wallet。这 12 个单词就是你的 wallet：**请确保你处在安全环境中，远离窥视，并准备好笔记本或纸张来抄写单词，然后再把它们放到安全位置**（例如保险箱）。点击 `Back Up Now`，查看这 12 个单词。

**还要写下单词的准确顺序：1、2、3 等；为了以后更容易阅读，可以用大写抄写，但请记住，如果将来需要手动输入，必须使用小写**。

![img](assets/13.webp)

抄写并安全保存这些单词后，继续 starter kit。所有后续设置都在指南末尾。

# TRANSACT 菜单
使用 wallet 非常简单：
- 进入 `Transact` 菜单
- 有两个主要命令：`Send` 和 `Receive`（**忽略 `Buy`**）。

![img](assets/17.webp)

当你有交易后，它们会显示在命令下方。因为现在没有资金，要开始接收，可以选择 `Receive`。

会出现一系列 *Assets*，但只关注 Bitcoin。你可以在 Bitcoin onchain（橙色图标）和 Liquid（蓝色图标）之间选择；Liquid 可以让你享受即时支付，类似 Lightning Network，但通过一种我们稍后会看到的机制。

开始时选择 Bitcoin Onchain，也就是橙色图标。

![img](assets/18.webp)

屏幕上出现的是一个 QR 码，代表你的一个 Bitcoin 地址；底部也能看到它，以 `bc1q` 开头并跟随其他字符。你可以把 QR 码展示给需要付款给你的人，以接收第一笔资金，通常是较小的 Bitcoin 份额，也称为 `Satoshi`。

![img](assets/19.webp)

如果返回并选择 Liquid，菜单会显示 ⚡️**Lightning Ready**。你需要知道，通过使用 `SWAP` 服务，Blockstream App 可以让你接收几乎即时的付款、发出 Lightning Network 付款请求或支付 LN invoice，并在同一 wallet 的 Liquid 账户中存入/取出资金。

![img](assets/20.webp)

在选择后打开的菜单中，选择你希望接收资金的方式：Liquid 或 Lightning。如果选择 Liquid，会显示一个类似 Bitcoin Onchain 的 QR 码，它代表一个以 `lq1q` 为前缀的地址。

如果选择 Lightning，系统会要求输入你想接收的金额，并点击 `Confirm` 确认。

![img](assets/21.webp)

Blockstream App 会显示代表 LN invoice 的 QR 码，可用任何 Lightning Network wallet 支付。

![img](assets/22.webp)

---
⚠️ 在我们的模拟中，我们请求接收 210 sats，但生成的 QR 码提示我们将收到 160 sats。Swaps 确实有成本，每次收到付款约 50 satoshis。**尤其在接收微支付时，务必记住这一点**。付款人没有变化：他会看到设置时请求的金额 210 satoshis 被扣除。

---

# 你是商家吗？使用 POS
为了让本指南成为真正的 **starter kit**，我们可以把这个 wallet 上的 Bitcoin 收款与外部 POS 结合起来。

你可以直接在 https://btcpos.cash/ 通过几个简单步骤完成配置。

![img](assets/23.webp)

这样你可以把 Lightning 付款直接收到用 Blockstream App 创建的 wallet 中，与协作者分享链接；为此只需按照接下来的步骤创建一个链接，并把它保存在手机主屏幕上方便使用。你需要复制 wallet 的 `Descriptor`，并粘贴到该链接页面中央的大输入区域。

# 1. 在 Liquid 网络上接收第一笔资金
必须在 wallet 的主屏幕启用 *Assets* 显示。如果它刚刚创建，你需要收到一个 LN invoice 的付款，或者在 Liquid 地址上接收资金。

收到资金后，你可以在 `Home` 菜单中看到的 `Assets` 里选择 Liquid。

![img](assets/24.webp)

# 2. 访问必要参数
现在你已经具备访问参数的条件，这些参数将允许把你的 wallet “搬运”到 POS。从技术上讲，这叫 *公钥导出*，这是你通过深入学习会掌握的细节。现在只需选择右上角菜单：

![img](assets/25.webp)

然后在出现的下拉菜单中选择 `Watch-only`。
![img](assets/26.webp)

会出现 `Output Descriptors`，这正是我们要找的参数。用相应命令复制它，然后回到正在配置 POS 的网页。

![img](assets/27.webp)

# 3. 配置 POS
把 descriptor 粘贴到相应区域，然后点击 `GENERATE POS LINK`。系统会创建一个唯一 URL，只对你和你的 wallet 有效。

![img](assets/28.webp)

你也可以先设置参考货币，在显示 `Currency` 的下拉菜单中选择 USD、CHF 或 EUR。
![img](assets/29.webp)

# 4. 通过 POS 生成付款请求来收款
点击 `GENERATE POS LINK` 后，页面会显示结果：**链接已成功创建**。你可以复制它，因为这个链接在生成的 URL 上将始终**只适用于你的 wallet**。

![img](assets/30.webp)

你也可以打开 POS 并开始使用：
![img](assets/31.webp)

例如，假设你想生成一张 3,351 sats 的 invoice，并附带描述。

![img](assets/32.webp)

点击 `CREATE INVOICE` 后，POS 会显示 QR 码或文字 invoice，供潜在客户支付。

![img](assets/33.webp)

当客户支付 invoice 后，他会正确看到 *description*（本例中为 Coppa del Nonno），POS 会显示已收到付款。

![img](assets/34.webp)

这也能在 wallet 中正确看到。
![img](assets/35.webp)

现在只需要记住并保存 POS 链接，在需要时使用，即使是在安装了 wallet 的同一部手机上。

![img](assets/36.webp)

把它作为链接/app 添加到主屏幕

![img](assets/37.webp)

# ⚠️ 重要说明
如果你重新阅读刚才关于最后一个示例中 invoice 收款的步骤，会注意到两件重要的事：
1. 客户看到的是 3,351 sats 的 invoice
2. 我们的 wallet 收到了 3,293 sats。

在感到惊讶之前，需要回到 POS 初始屏幕，它显示了下图中的说明：

![img](assets/38.webp)

3,351（提交给客户的 invoice）和 3,293（你的收款）之间的差额正是这些：
- 每个生成的 invoice 收取 50 sats
- 0.25% 服务费（8 sats = 3,351 的 0.25%）
- 总收款：3,293

#### 你刚刚起步，而这是一个 starter kit。小额费用是为了以 self-custody、无中介的方式使用 Bitcoin，并享受包括小额即时支付在内的各种机会所做的折中。

#### 通过学习，你会学会使用其他工具，它们不会要求超出资深用户通常也会承担的费用。

---
# 其他设置

现在该好好了解你的第一个 wallet。设置很重要，因为它们会帮助你的日常使用。

## 菜单
Blockstream App 的菜单位于底部，包括：
- Home
- Transact
- Security
- Settings

从 `Security` 菜单继续配置你的 wallet。除了查看和抄写 `Recovery phrase` 单词外，此菜单还提供其他重要功能。

例如，你可以设置通过生物识别控制登录 wallet（如果手机上已设置），也可以添加六位 PIN 来访问 wallet。这些选项非常重要，因为如果别人拿到你的手机，它们能防止对方访问和查看你的 wallet。

![img](assets/14.webp)

在此菜单中，你还可以决定 *Logout* 时间，也就是 wallet 在几分钟无操作后断开连接的时间。默认设置为 *5 minutes*，你可以根据需要把它调长或调短。
![img](assets/15.webp)
# SETTINGS 菜单
这是非常重要的菜单，因为它包含所有 wallet 设置。点击此菜单后，你可以例如重命名 wallet：在我们的示例中，它被命名为 *Starter Kit*。当同一设备上使用多个 wallet 时，重命名以便区分非常重要。

![img](assets/39.webp)

如果进入 `Denomination` 子菜单，可以找到有关货币的非常有用的设置。
![img](assets/40.webp)

我建议使用 `satoshi/sats` 作为 Bitcoin 金额单位。Satoshi 是 BTC 的最小单位，等于一亿分之一 Bitcoin。此外，还会出现用于换算的参考 exchange 选择。使用一个可以以 EUR 显示和设置金额的选项。

![img](assets/41.webp)

最后，在 `Settings` 菜单中，你可以检查当前使用的 Blockstream App 版本、查看是否需要更新，并使用命令直接 *in-app* 请求支持。
![img](assets/42.webp)

# HOME 菜单
Blockstream App 的 `Home` 是每次访问时 wallet 打开的菜单。向下滚动，你会看到通过内置 exchange 购买 Bitcoin 的选项。**不要使用它**。

![img](assets/16.webp)

# Wallet 恢复
如果在使用过程中你发现需要换手机，或者需要在多个设备上使用 *Starter Kit* wallet，Blockstream App 可以做到。

要继续，你只需要学习下面说明的 wallet 恢复流程，其中包括在失去最初使用 wallet 的手机访问权限时应采取的步骤。

事实上，你的资金并不在“设备上”，也不在“wallet 里”。资金在 Bitcoin 网络上，无论是 Onchain、Lightning 还是 Liquid。准确地说，wallet 的公钥和私钥才是访问已使用地址及其相关余额的工具。

正是为了这个流程，你才抄写了 12 个单词并把它们放在安全处……**你做了，对吗？** 因为没有这些单词，你将无法再访问资金。

# a. 重新安装 Blockstream App
首先按照开头展示的流程重新安装 Blockstream App。期间可能已经有新的 release，请使用最新版本。

在新设备上启动 Blockstream App，点击 `Get Started`，并拒绝数据收集请求。

# b. 从备份恢复
与第一次安装的相似之处到此为止。当出现 wallet 创建屏幕时，不要像第一次那样选择 `Set Up Mobile Wallet`，而要选择 `Restore from backup`。

![img](assets/43.webp)

如果你使用 Bitcoin 主网，也就是使用真实资金的网络，在下一屏选择 `Mainnet`。

![img](assets/43.webp)

屏幕会显示输入 `Recovery phrase` 单词的框。按顺序、正确地重新输入它们，然后选择 `Continue`，在新设备上重新创建 wallet。

![img](assets/45.webp)

Wallet 恢复阶段可能需要几分钟；请耐心等待它成功完成。流程结束后，你会再次看到你的 wallet，以及余额和交易历史。

![img](assets/46.webp)

---
⚠️ 在新设备上重新创建的 wallet 是 100% 活跃的。这意味着它也拥有用于花费的私钥。如果你想把它交给业务协作者，请记住这一点。

**对于协作者，最好使用 POS 链接，因为它只使用公钥（`descriptor`）创建**。

---

# 如何继续学习？

![img](assets/47.webp)
![img](assets/48.webp)
