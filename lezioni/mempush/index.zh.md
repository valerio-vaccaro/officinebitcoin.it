---
layout: default
title: "MemPush：轻松发送和管理 mempool 中的 Bitcoin 交易"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only 课程</span> <span>本项目由 valerio-vaccaro 维护</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# MemPush：轻松发送和管理 mempool 中的 Bitcoin 交易

MemPush (https://mempush.com/) 是一个创新平台，让在 mempool 中发送和管理 Bitcoin 交易变得简单、安全且易于使用。mempool 是等待在 blockchain 上确认的 Bitcoin 交易的临时“蓄水池”，也是这项服务的核心；该服务为用户和开发者消除了技术复杂性。

## 什么是 MemPush？

MemPush 是一项 Web 服务，允许你将 raw Bitcoin transactions（十六进制格式）直接发送到 mempool，无需高级配置或个人 Bitcoin nodes。MemPush 由 Valerio Vaccaro 设计，同时支持 Tor 网络，为用户提供更强的隐私保护。

![alt text](https://officinebitcoin.it/lezioni/mempush/front.png)

源代码以 open-source 许可证发布在 GitHub (https://github.com/valerio-vaccaro/mempush)，任何人都可以验证项目安全性、参与开发，或托管该服务的个性化实例。

## MemPush 如何工作？

MemPush 的界面直观且易于使用：

1. **访问网站**：访问 https://mempush.com/。
2. **输入 raw transaction**：将十六进制格式的 Bitcoin 交易粘贴到专用字段中。
3. **发送交易**：点击 "Submit Raw Transaction"，通过 Bitcoin nodes 将交易传播到 mempool。
4. **监控状态**：使用 blockchain explorer 查看交易进度。
5. **自动重新广播**：如有必要，MemPush 会自动重新广播交易，以确保它们留在 mempool 中。

![alt text](https://officinebitcoin.it/lezioni/mempush/list.png)

无需注册，open-source 方式也消除了隐藏风险，因此 MemPush 即使对经验较少的用户也很理想。

## MemPush 适合谁？

MemPush 旨在满足多种需求：
1. **低手续费**：低手续费交易会被自动重新广播，以防止它们在流量高峰期间从 mempool 中被移除。
2. **Timelocked 交易**：支持监控和重新广播带有时间约束的交易，确保这些交易得到有效管理。
3. **高级监控**：MemPush 会定期检查交易状态，只允许移除已确认或已失效的交易（例如 double-spends）。
4. **增强隐私**：借助 Tor 网络支持，MemPush 在发送交易时保护用户匿名性。

## 技术特性

GitHub repository (https://github.com/valerio-vaccaro/mempush) 展示了一个优雅的 Python 实现，它基于 Flask framework，并集成数据库用于交易管理。MemPush 依赖 blockstream.info 和 mempool.space 等服务来监控和传播交易，未来计划集成本地 Bitcoin node。

主要优势：
- **安全性**：不存储敏感数据或私钥，确保全面保护。
- **可扩展性**：通过与 Bitcoin 网络的直接连接，支持高交易量。
- **Open-source**：公开代码允许社区进行验证、贡献和定制。

## 结论

对于任何希望无复杂操作地在 mempool 中发送和管理 Bitcoin 交易的人来说，MemPush 都是一个强大且易于使用的解决方案。凭借其透明性、隐私支持和易用性，它为 Bitcoin 生态系统提供了有价值的补充。访问 https://mempush.com/ 进行试用，或在 https://github.com/valerio-vaccaro/mempush 查看代码。
