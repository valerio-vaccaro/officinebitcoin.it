---
layout: default
title: "本教程的前提条件"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only 课程</span> <span>本项目由 valerio-vaccaro 维护</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

![cover](https://officinebitcoin.it/lezioni/verifica/1cover.webp)
验证加密签名是一项基础安全实践，**每一位 open-source 软件用户都应该把它纳入自己的良好习惯流程**。

Open source 从本质上说是可修改的，这意味着理论上任何人都可以在你学习 Bitcoin 协议并用来练习的应用程序中引入 backdoors、攻击或恶意代码。

作为正在深入学习的用户，你有机会亲自验证下载的软件是否被篡改，并且你应该在安装和使用它之前这样做。

在开始之前，我们也把 Officine Bitcoin 演示中的一个经典带来：meme。这不会是一场沉重的演示，但让我们从一开始就放松一下气氛。

![meme](https://officinebitcoin.it/lezioni/verifica/2meme.webp)

## 如何操作？
开发者总是会在发布新的软件版本时附带一个加密签名。
这意味着，除了更新软件之外，他们还会发布它，并认证自己已将它绑定到某个特定 fingerprint。提醒：用私钥生成的数字签名是唯一且不可修改的。

你只需要 GPG suite，就可以进行签名验证。

![img](https://officinebitcoin.it/lezioni/verifica/3.webp)

# 本教程的前提条件
- 简要回顾非对称加密
- 需要验证的元素：
  - software (binary, apk, etc.)
  - 开发者的数字签名，通常是一个 `.asc`、`.sig` 文件或一个 checksum。
- 用于验证的工具：
  - GPG suite
  - 一个终端（Linux 和 Windows 都可用）
# 非对称加密

![img](https://officinebitcoin.it/lezioni/verifica/4.webp)

这里有两把彼此相关的密钥：一把公钥和一把私钥。顾名思义：
- 公钥可以自由获得，并可与任何人共享。
- 私钥由其所有者安全保管。

用公钥加密的数据只能由对应的私钥解密。这使任何人都可以向密钥对的所有者发送加密数据，而不需要事先共享秘密部分。

公钥加密比对称加密更慢，不适合加密大量数据。不过，它允许安全地分发加密密钥。
公钥加密中常用的一些算法包括 RSA、ECC、ElGamal 和 DSA。

## 开发者一侧：新更新

开发者发布 open source 代码，而代码本质上不是加密的。
他们创建一个加密 hash（生成 `checksum`），并用自己的私钥加密 digest：这就创建了签名，也就是前面提到的 `.sig` 或 `.asc` 文件。

完成这个过程后，开发者会把两个文件都上传到网站或 GitHub repository。你的下载就是从那里开始的。

![img](https://officinebitcoin.it/lezioni/verifica/5.webp)

然后你需要开发者的公钥。有时它在 GitHub repository 中，有时在公共服务器（*keyservers*）上。即使搜索可能需要一些努力，公钥也是验证软件的关键元素，所以请努力获取它。

如果你遇到困难，可以在 Officine Bitcoin Telegram 群组提问，在那里你会找到获取特定公钥的说明。

![img](https://officinebitcoin.it/lezioni/verifica/6.webp)

为了验证数据完整性，接收者使用发送者的公钥解密签名，并得到一个结果：

a. 数据被认为是真实的，并且在传输过程中未被修改。
b. 数据可能已被篡改。

通过用私钥加密 hash 值，**PGP 签名保证 checksum 本身受到保护，并与发送者身份相关联。这可以防止在被篡改的数据上伪造签名**。

签名可以用来验证任何东西：文件、emails、文档和软件下载。检查 PGP 签名时，你证明数据确实来自可信来源并且保持完整。

现在你将能够验证一个移动 apk。

我们以 Phoenix 的下载为例，它是一个 non-custodial LN wallet，这样我们就能在未来某个 Officine Bitcoin 晚上专门介绍它。

# 下载并验证 Phoenix Wallet (Acinq)
如果你已经访问过 Phoenix 开发者 [Acinq](https://phoenix.acinq.co/) 的网站，就已经知道 Android 和 iOS 的官方 stores 中都提供下载。
也许你从未注意到，但 Android 的 apk 文件也可以下载。

![img](https://officinebitcoin.it/lezioni/verifica/8.webp)

[我们去那里！](https://github.com/ACINQ/phoenix/releases) 找到你将用 `wget` 下载的 `apk` 和 `Signature` 文件。
在 Phoenix 的情况下，用于验证的签名文件名为 **`SHA256SUMS.ASC`**。

![img](https://officinebitcoin.it/lezioni/verifica/9.webp)

同一个 repository 中也有说明，教你下载对应 *signing key E04E48E72C205463* 的公钥（Drouinf 密钥的唯一 fingerprint）。
复制链接并用 `wget` 下载，或者按照 repo 相应部分中建议的说明操作。

![img](https://officinebitcoin.it/lezioni/verifica/10.webp)

---
⚠️**公钥必须导入，而不仅仅是下载**。
⚠️ 文件下载必须发生在同一个目录中。

---
# 打开终端
使用终端，进入 apk 和 `SHA256SUMS.ASC` 文件下载所在的目录，并按顺序运行命令。

![img](https://officinebitcoin.it/lezioni/verifica/11.webp)

![img](https://officinebitcoin.it/lezioni/verifica/12.webp)

当验证返回 positive 结果时，你可以把 apk 传输到手机上并安装 app。

---
# 困难的验证
签名验证不容易可能有几个原因，而且几乎总是由于混乱或经验不足：
1. apk 和/或 .asc 文件被下载了多次，因此在目录中会以例如 **filename-1** 或 **filename(1)** 这样的奇怪名称出现
2. apk 和 .asc 不在同一个目录中
3. 公钥已下载，但没有导入到 gpg keyring 中。

还可能出现其他情况，即使操作正确，验证也会失败。
重要的是查看终端中出现的错误，复制它，然后在互联网上搜索解决方案。

# 使用 Sparrow Wallet 验证
如果你已经使用 Sparrow Wallet，可以继续用这个软件验证下载，**但它本身的下载和安装必须先经过认真而严格的 GPG 验证**。

启动 Sparrow wallet，并在 `Tools` 菜单中查找 `Verify Downloads`。

![img](https://officinebitcoin.it/lezioni/verifica/13.webp)

一个界面会打开，要求你插入刚刚下载的文件。点击 `Browse` 会打开文件管理器，把每个文件加载到所需字段中。

![img](https://officinebitcoin.it/lezioni/verifica/14.webp)

有时界面表单会自动填写。如果没有，请用相应文件填写所有字段。

![img](https://officinebitcoin.it/lezioni/verifica/15.webp)

positive 结果会通过绿色对勾以及 *`Ready to install`* + < filename > 确认以图形方式显示。

# 学习支持
如果你参加了 Telegram 上的现场演示，可以把它视为迈向个人主权（不只是金融主权）的又一步。
如果你错过了，**不要绝望**：这些笔记正是用来补上的，而且你还应该知道，我们会在 Officine 再次提出这个主题。

为了不错过下一次演示，请加入 [Telegram group](https://t.me/officinebitcoin)，保持持续更新。

![img](https://officinebitcoin.it/lezioni/verifica/17.webp)

你也可以找到离你最近的 [Satoshi Spritz](https://satoshispritz.it/)。Satoshi Spritz 是一个本地 meetup，只讨论 Bitcoin，你可以带着问题去，并从其他经验丰富的 bitcoiners 那里得到回答。在链接中你会找到半岛地图。

![img](https://officinebitcoin.it/lezioni/verifica/16.webp)

最后，如果你附近没有 meetup，可以利用 [SatoshiSpritz Connect](https://t.me/SatoshiSpritzConnect) 的每周直播。这是一个虚拟 meetup，为无法参加 Satoshi Spritz 的人创建，也用于帮助较小的 meetups 做笔记并为自己的演示寻找灵感。

![img](https://officinebitcoin.it/lezioni/verifica/18.webp)
