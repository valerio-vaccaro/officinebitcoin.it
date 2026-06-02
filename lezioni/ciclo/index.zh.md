---
layout: default
title: "Bitcoin 交易生命周期"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only 课程</span> <span>本项目由 valerio-vaccaro 维护</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Bitcoin 交易生命周期

## 什么是 Bitcoin 交易
Bitcoin 交易是记录在 blockchain 上的一项操作，它把价值从一个或多个输入（先前收到的资金，称为 UTXOs - Unspent Transaction Outputs）转移到一个或多个输出（新的接收者）。
输入是过去交易中尚未花费的输出，而输出会把 satoshis 分配到特定地址。一个例外是 "coinbase" 交易，它是每个区块中的第一笔交易，可以在没有输入的情况下产生新的 bitcoins（挖矿奖励和手续费）。如果某个输入中的资金没有全部花完，差额 (change) 会通过一个额外输出返回给发送者；如果没有正确处理，就会永久丢失。

## 生命周期阶段
交易生命周期如下：

- 创建：Wallet 会根据要发送的金额和降低手续费的策略，选择要花费哪些 UTXOs 来构建交易。如果输入金额大于输出金额，就会生成一个 "change" 输出返回给发送者，但这会增加交易大小和成本。有些 wallets 会尝试避免这种情况。
- 签名：交易会为每个输入使用一个或多个数字签名进行签署，从而完成认证。这个步骤对交易有效性至关重要；在 multisig 交易中，它可能涉及多个参与方。
- 广播：已签名的交易被发送到网络（"broadcast"），并插入本地 node 的 mempool。mempool 会根据共识规则（例如有效签名、可用资金）和本地规则（例如为防止 spam 而设置的 400 KB 最大大小）验证交易。随后，该 node 会把交易传播给 peers；这些 peers 会验证交易并插入自己的 mempools，形成级联式广播。由于配置或连接不同，各 node 的 mempool 可能并不相同。
- 确认：矿工把交易纳入一个区块，从而在 blockchain 上确认它。不过，在获得更多确认（后续区块）之前，它仍然可能受到替换或 forks 的影响。低手续费交易可能在 mempool 中停留很久或被丢弃，但如果输入仍未花费，即使几个月后也仍可能被挖出。

## 问题处理
- 交易从 mempool 中消失：如果低手续费交易被移除（例如因为流量激增），可以使用 TXID 手动重新传输（rebroadcast），甚至可以借助 scripts 或 explorers。有人也可能代表第三方这样做。
- Replace-by-Fee (RBF)：如果手续费不足，只要交易带有 RBF flag，就可以用一笔支付更高手续费的交易替换它。有一项提议认为，所有交易都应该默认可替换，因为矿工无论如何都会偏好更高的手续费。
- Child Pays for Parent (CPFP)：如果不能使用 RBF（例如这不是你自己的交易，或资金已经耗尽），可以用一笔新的高费交易花费卡住交易的某个输出，让两笔交易都对矿工有吸引力。手续费总和必须覆盖两笔交易。若节点丢弃第一笔交易，导致链条断开，就会出现问题；一个正在开发中的协议旨在传输交易包，以避免这种情况。

## 最终确认
只有在获得多次确认（其上方已有多个区块）后，交易才被视为最终确定。单次确认并不足够，因为 forks 或双花可能使其失效。White Paper 建议 6 次确认（约 60 分钟，区块平均每 10 分钟产生一次），但具体数量会随金额和风险而变化。区块时间的波动很大，但平均值会通过挖矿难度维持。

## 结论
当交易被“刻入” blockchain，永久记录这次价值转移时，这个周期就结束了。

## 程序
本课程是为 Satoshi Spritz Connect 创建的。
