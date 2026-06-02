---
layout: default
title: "挖矿简介"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only 课程</span> <span>本项目由 valerio-vaccaro 维护</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# 挖矿简介
Bitcoin 挖矿是协议中的一个基础过程，用来为 mempool 中的交易提出一种顺序，选择其中一个子集来创建新区块，并更新 blockchain 的状态。

挖矿被设计成去中心化且随机的过程（加上引号，是因为它基于一个密码学谜题），从而避免对交易进行中心化管理。

## 挖矿的目的
挖矿解决与中心化有关的问题，例如：

- 审查：中心化实体可能会阻止某些交易，但在去中心化矿工存在的情况下，交易更有机会被纳入区块。
- 双花：如果没有可被腐化的矿工，就很难重写历史，或牺牲一笔交易来偏袒另一笔交易。
- Timestamping：提供一种安全且共享的时间顺序，它不依赖中心化权威，而依赖矿工和节点之间的共识。

# 挖矿如何运作
挖矿过程可以逐步说明：

- 交易选择：矿工从 mempool 中选择交易，通常优先选择手续费更高的交易，以优化收益（这是一个 NP-complete 问题，类似于 "knapsack problem"）。
- Coinbase 构造：矿工创建一笔特殊交易（coinbase），将区块奖励（目前为 3.125 BTC，每四年减半）以及所选交易的手续费分配给自己。
- Merkle Root：所选交易被组织成一种树形数据结构（Merkle Tree），生成 Merkle Root，也就是一个代表所有交易及其顺序的 hash。
- Block Header：矿工构建区块头原型，其中包括：
1. timestamp。
2. 前一个区块的 hash。
3. Merkle Root。
4. 难度（target），它取决于网络。
5. nonce（随机数，例如初始化为零）。
- 密码学谜题：矿工对区块头应用两次 SHA-256 算法，并检查结果是否有足够数量的前导零（低于难度阈值）。如果没有，就修改 nonce 或其他字段（例如 timestamp 或交易顺序），然后重复计算。由于 SHA-256 的性质，这是没有捷径的暴力尝试工作。

## 优化
为了加快过程，矿工可以对区块头的前 64 个字节（不可变部分）计算第一次 SHA-256，然后只在剩余部分上迭代，改变 nonce。专业化已经带来了每秒可执行数十亿次尝试的 hardware（ASIC）。

# 验证过程
当矿工找到一个解时，会把完整区块（区块头 + 交易）传输到网络。节点会验证：
- 区块头 hash（一次 SHA-256 用于确认）。
- 区块信息的正确性（timestamp、前一个区块的 hash、Merkle Root 和 nonce）。
- 在检查所有相关交易正确性之后，Merkle Root 是否可复现。

如果有效，该区块会被加入 blockchain。奖励（coinbase + 手续费）只有在 100 次确认后（约 16 小时）才能花费，以确保稳定性。

# 挖矿成本和奖励
成本：

- 电力：主要的可变成本。
- Hardware：昂贵且寿命短的 ASIC，很快会被更高效的型号取代。
- 基础设施：冷却、安装、维护（例如，太阳能板并不是“免费”的）。

奖励：

- 固定奖励（在 2024 年减半为 3.125 BTC）。
- 可变的交易手续费。

矿工必须遵守共识规则：无效区块会被丢弃，资源被浪费且没有奖励。即使是有效区块，如果另一个矿工赢得竞争，也可能变成“孤块”，从而造成损失。

## 经济策略
挖矿具有竞争性：矿工会尽量最大化在线运行时间，以摊销固定成本。临时性使用（例如只在有剩余能源时开启矿机）并不实际，因为初始成本要求持续运行。投资回报可能漫长且不确定。

# Solo 和 Pool 挖矿

- Solo Mining：矿工独自工作，使用完整节点或自定义软件构建区块。如果找到一个区块，就获得全部奖励，但概率极低（使用单台 ASIC 可能需要几个世纪）。
- Pool Mining：Stratum 等协议允许矿工协作：
1. pool 提供一个模板（coinbase、Merkle Root 等）。
2. 矿工发送 shares（带有一定数量零、低于区块难度的尝试）作为工作证明。
3. 当 pool 中的矿工找到一个区块时，奖励按发送的 shares 比例分配。
- Stratum v2：一种演进，允许矿工选择交易，减少 pool 的中心化，尽管它需要检查来确保正确性（例如，给 pool 的手续费）。

# Hashrate 估算
Hashrate（算力）的估算方式：
- 在 pool 中：统计单位时间内收到的 shares，再乘以 share 难度。这是一种会受运气扰动的估算。
- 全网：使用 Bitcoin 的难度和区块之间的平均时间（约 10 分钟）。波动是正常的，但平均值可靠。

像 Nerd Miner 这样的 hardware 使用内部计数器获得精确数据，而 pool 依赖更可变的估算，这会体现在波动的图表中。

# 课程
本课是为 Satoshi Spritz Connect 创建的。
