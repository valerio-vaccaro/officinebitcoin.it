---
layout: default
title: "Bitcoin 描述符"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only 课程</span> <span>本项目由 valerio-vaccaro 维护</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Bitcoin 描述符

## 简介

## 描述符
描述符是一个相对较新的概念，目前还不算普及，但它们很适合用来描述 Bitcoin wallet 的结构。描述符是可读的字符串（包含字母数字字符、十六进制字符，以及括号等少量符号），用于以清晰且标准化的方式表示一个 wallet，也就是计算余额、接收和花费 Bitcoin 所需的一组公钥和私钥。

## wallet 管理的演进
为了说明描述符的背景，讲者回顾了 wallets 的演进：

- 早期 wallets（pre-BIP-32）：在早期，使用 Bitcoin Core 时，wallets 是包含随机生成密钥的文件。每当地址用完，就会加入新的地址，因此需要频繁备份，以免丢失资金。这个系统效率很低。
- BIP-32 (HD Wallet)：随着分层确定性生成方式的引入，一个 seed 会生成主密钥，所有地址都从这个主密钥派生出来。只备份 seed 就足够了，但这还不是一个完整的解决方案。
- Mnemonics (BIP-39)：随后，seed 由 12 个或 24 个词组成的序列（mnemonic）派生而来，更容易保存。不过，要重建一个 wallet，还需要派生路径的信息（例如 Legacy、SegWit），否则资金可能无法恢复。

仅有 mnemonic 还不够，尤其是对于 multisig（需要多个签名）这类复杂 wallets，或者带有高级 scripts 的 wallets（例如 timelock 或继承条件）。有些 wallets 会尝试所有可能的派生路径来寻找资金，而另一些 wallets（例如 Electrum）则要求指定 wallet 类型。此外，在 multisig 中，还需要其他参与者的公钥，这进一步增加了备份的复杂度。

## 什么是描述符，以及为什么需要它们
描述符的出现是为了解决这些限制，为 wallet 结构提供完整而灵活的描述。它们不会取代 mnemonic，而是对其进行补充，包括：

- 扩展公钥（xpub、ypub 等）。
- 派生路径（例如 Legacy 的 m/44'/0'/0'）。
- 任何花费 scripts 或条件（例如 multisig、timelock）。

## 实际示例
- Legacy single-sig：一个简单的描述符可能是 `pk([fingerprint/derivation]xpub...)`，其中：
1. pk 表示一个公钥。
2. [fingerprint/derivation] 指定主密钥和路径。
3. xpub 生成地址（例如，0/* 用于接收，1/* 用于 change）。
- Multisig：一个例子是 `sortedmulti(2, xpub1, xpub2, xpub3)`，它描述一个 2-of-3 wallet，并对密钥排序以保持一致性。
- 复杂 scripts：使用 p2sh (pay to script hash) 或 p2wsh (pay to witness script hash) 这样的 scripts 时，可以加入高级条件，例如 timelock 或逻辑组合 (and, or)。

## 描述符与 Taproot
一个有意思的例子是 Taproot (tr) 的描述符，它支持两种花费模式：

- 使用特定密钥直接签名。
- 一棵条件树（例如继承或 timelock），在花费之前将复杂性隐藏在 blockchain 上。

## 描述符的优势
- 完整备份：它们包含重建 wallet 所需的全部信息，无需反复尝试。
- 兼容性：非常适合 watch-only wallets，在没有私钥的情况下监控资金。
- 灵活性：支持 single-sig、multisig 和复杂 scripts。
- 隐私：不会泄露秘密，可以像 xpub 一样共享。

## 限制和兼容性
并非所有 wallets 都完全支持描述符。例如，Bitcoin Core 只实现了其中一个子集，并且需要为地址和 change 分别使用两个描述符。Sparrow 或 Specter 等软件提供了更好的支持，允许导入/导出描述符并可视化其结构。

可以使用以下工具进行实验：
- Sparrow：支持描述符，并提供图形界面来创建或分析它们。
- BDK：带有命令行界面的库，用于管理复杂描述符。
- Testnet/Signet：安全的测试环境，可以在不冒真实资金风险的情况下测试。

## 参考资料

- [BIP-380](https://github.com/bitcoin/bips/blob/master/bip-0380.mediawiki)
- [Bitcoin Improvement Proposal 380](https://github.com/bitcoin/bips/blob/master/bip-0380.mediawiki)
- [Bitcoin Improvement Proposal 380](https://github.com/bitcoin/bips/blob/master/bip-0380.mediawiki)

## 课程
本课程是为 Satoshi Spritz Connect 创建的。
