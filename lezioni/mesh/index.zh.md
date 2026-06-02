---
layout: default
title: "**Mesh Networks** 入门以及 LoRa 与 **LoRaWAN** 详细分析"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only 课程</span> <span>本项目由 valerio-vaccaro 维护</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# **Mesh Networks** 入门以及 LoRa 与 **LoRaWAN** 详细分析

## **Mesh Networks** 入门

**Mesh Networks** 是一种网络架构，其中节点（设备）以非层级方式互相连接，使每个节点都可以不经过 router 或 gateway 这样的中心点而直接与其他节点通信。每个节点都有可能同时充当发送方和接收方，数据也可以通过多条路径转发以到达目的地。

这种结构提供了几个优势：

- **韧性**：如果某个节点失效，数据可以通过其他节点重新路由，从而保证通信连续性。
- **可扩展性**：**Mesh Networks** 可以通过添加新节点轻松扩展，而无需对基础设施进行重大修改。
- **扩展覆盖范围**：数据转发可以覆盖比传统网络更大的区域。
- **灵活性**：适用于多种应用，从 Internet of Things (IoT) 到家庭和工业网络。

不过，**Mesh Networks** 也带来一些挑战：

- **复杂性**：管理多条路径并协调节点会增加复杂性。
- **能耗**：转发数据的节点会消耗更多能量，从而缩短电池寿命。
- **容量有限**：在密集网络中，multi-hop 传输可能引入延迟并降低整体容量。

**Mesh Networks** 被用于 **Zigbee**、**Bluetooth** Mesh、**Thread** 等无线技术中，也在某些情况下用于基于 LoRa 的专有协议。对于低功耗、长距离网络而言，最相关的技术之一是 **LoRaWAN**，它采用了不同于传统 mesh 拓扑的方法。

## **LoRa** 与 **LoRaWAN**：背景和差异

### **LoRa**

**LoRa** (Long Range) 是一种扩频调制技术，源自 Chirp Spread Spectrum (CSS) 技术，由 Cycleo 开发（Semtech 于 2012 年收购）。

**LoRa** 代表无线网络的物理层 (PHY)，定义数据如何在免许可频段上调制和传输（例如欧洲 868 MHz、北美 915 MHz、某些地区 433 MHz）。

其主要特征是：
- 长距离传输（农村地区最高可达 15 km，城市地区 2-5 km）。
- 极低能耗，适合低数据速率和长电池寿命的 IoT 应用。

### **LoRaWAN**

**LoRaWAN** (Long Range Wide Area Network) 是一种基于 LoRa 的 MAC (Media Access Control) 层协议，由 LoRa Alliance 开发。LoRa Alliance 是一个成立于 2015 年的非营利协会，拥有 500 多个成员，包括 Semtech、Cisco、IBM 和 Orange。

**LoRaWAN** 定义：
- 网络架构。
- 通信协议。
- 传输频率、数据速率、安全性和互操作性等方面。

不同于只处理信号调制的 LoRa，**LoRaWAN** 规定设备（终端节点）如何与 gateways 通信，以及 gateways 如何通过 backhaul 连接（例如 Ethernet、Wi-Fi 或 cellular）连接到网络服务器。

#### **Mesh Networks** 与 **LoRaWAN** 的比较

不同于传统 **Mesh Networks**（例如 **Zigbee**、**Bluetooth**），**LoRaWAN** 使用星型拓扑，其中终端节点直接与 gateways 通信，gateways 再把数据转发到中央网络服务器。下面是详细比较：

1. 网络拓扑
**Mesh Networks**：节点充当中继器，转发数据以扩展覆盖范围。这会增加复杂性和能耗。
**LoRaWAN**：星型拓扑，节点直接向 gateways 传输。这消除了中继节点，简化网络并降低能耗。

2. 能耗
**Mesh Networks**：中继节点消耗更多能量，缩短电池寿命。
**LoRaWAN**：终端设备只在必要时传输（例如使用 ALOHA 的 Class A），可实现长达 10-15 年的电池寿命。

3. 范围和覆盖
**Mesh Networks**：范围通过 multi-hop 扩展，但每一跳都可能引入延迟并降低效率。
**LoRaWAN**：得益于 CSS 调制，无需中继节点即可提供最高 15 km（农村）或 2-5 km（城市）的范围。

4. 容量和可扩展性
**Mesh Networks**：在密集网络中，multi-hop 可能造成瓶颈并降低容量。
**LoRaWAN**：借助 gateway 冗余和星型拓扑，支持来自数千台设备的数百万条消息。

5. 安全性
**Mesh Networks**：安全性取决于协议（例如 **Zigbee** 使用 AES-128）。multi-hop 转发可能引入漏洞。
**LoRaWAN**：使用 AES-128 会话密钥进行 end-to-end 加密（Network Session Key 和 Application Session Key）。

6. 复杂性和成本
**Mesh Networks**：管理转发路径会增加复杂性。随着中继节点增加，成本可能上升。
**LoRaWAN**：星型拓扑更简单。Gateways 可能昂贵，但传感器便宜，免许可 ISM 频段降低了成本。

## **LoRa** 与 **LoRaWAN** 详细分析
### **LoRa**：物理层
**LoRa** 使用 Chirp Spread Spectrum (CSS) 调制，以频率变化的正弦信号编码数据，并将信号分布在更宽的带宽上以提高抗噪声能力。它提供高灵敏度（-110 dBm 到 -140 dBm），适合嘈杂环境。

主要参数包括：

- Spreading Factor (SF)：从 7 到 12，影响数据速率和范围。SF12 提供长距离但低 bitrate (0.3 kbps)；SF7 提供更高速度 (27 kbps)，但范围较小。
- Bandwidth (BW)：125 kHz、250 kHz 或 500 kHz，影响 bitrate 和稳健性。
- ISM 频率：863-870 MHz（欧洲）、902-928 MHz（北美）、433 MHz（其他地区）。

LoRa 适合小数据包 IoT 应用，例如环境监测、smart metering 和精准农业。

## **LoRaWAN**：协议和架构

**LoRaWAN** 定义三类设备：

- Class A：低功耗双向设备，具有 uplink 传输和短 downlink 接收窗口（ALOHA）。适合电池供电传感器。
- Class B：增加计划接收窗口（每 128 秒一次，通过 GPS beacon 同步），用于计划 downlinks。
- Class C：始终监听 downlinks 的设备，适合市电供电设备。

**LoRaWAN** 架构包括：
- 终端节点 (End Devices)：收集并传输数据的传感器或 IoT 设备。
- Gateways：从节点接收数据，并通过 backhaul 转发到网络服务器。
- Network Server：管理网络、消除重复数据，并为 downlinks 选择 gateway。
- Application Server：处理数据以用于分析或可视化。

## 使用 LoRa 的 **Mesh Networks**
虽然 **LoRaWAN** 使用星型拓扑，但可以通过外部协议使用 LoRa 调制来实现 mesh 网络。在 LoRa mesh 网络中，节点充当中继器以扩展覆盖范围，这在没有 gateways 的区域很有用。

然而，这需要：
- 自定义协议：**LoRaWAN** 原生不支持 mesh。
- 更高能耗：中继节点消耗更多能量。
- 复杂性：管理转发路径和避免冲突（例如 CSMA-CA）。

示例：LoRa 模块（例如 Semtech 的 SX1276）配合 ESP32 等微控制器，用于私有 **Mesh Networks**。

**LoRaWAN** 的优势

- 能源效率：星型拓扑消除中继节点。
- 简单性：与 gateways 直接通信。
- 可扩展性：支持数千台设备和数百万条消息。
- 安全性：使用 AES-128 加密提供稳健安全性。
- 互操作性：来自 LoRa Alliance 的开放标准。

**LoRaWAN** 的限制

- 低数据速率：0.3-50 kbps，不适合大体量数据。
- 延迟：Class A 会为 downlinks 引入延迟。
- Gateway 成本：对私有网络而言较高。

# 结论
**Mesh Networks** 通过 multi-hop 转发提供韧性和灵活性，但复杂且消耗更多能量。**LoRaWAN** 凭借其星型拓扑和 LoRa 调制，非常适合低功耗、长距离 IoT 应用，因为它简单、可扩展，并且电池寿命可长达 15 年。

在 **Mesh Networks** 与 **LoRaWAN** 之间选择取决于需求：mesh 适合节点彼此距离较近的环境，**LoRaWAN** 适合以最低能耗进行长距离通信。虽然 LoRa 可以实现 mesh，但与 **LoRaWAN** 相比并不常见；**LoRaWAN** 因标准化以及 LoRa Alliance 的支持而占据主导地位。
