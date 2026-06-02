---
layout: default
title: "Ghostinbox.it：无需邮箱地址也能使用电子邮件"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only 课程</span> <span>本项目由 valerio-vaccaro 维护</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Ghostinbox.it：无需邮箱地址也能使用电子邮件

Ghostinbox 是一个 web 平台，允许用户创建临时 email 地址来接收消息，而无需暴露自己的真实 email 地址。该服务非常适合快速注册、账户验证、email deliverability 测试，或任何你想避免 spam 或保护身份的场景。

与传统 email 服务不同，Ghostinbox 不要求注册，也不存储个人数据，因此很适合重视 privacy 的用户。此外，对 Tor 网络的支持允许匿名访问该服务，隐藏用户的 IP 地址。项目的 open-source 属性确保了透明度，并允许开发者检查代码中可能存在的漏洞或进行定制。

## Ghostinbox 如何工作？
![alt text](https://officinebitcoin.it/lezioni/ghostin/front.png)

使用 Ghostinbox 非常直观，也不需要技术技能：

1. **访问网站**：访问 https://ghostinbox.it/（或通过 Tor 访问以获得更高匿名性）。
2. **生成临时 email 地址**：点击按钮创建新的临时 email 地址（例如 random@ghostinbox.it）。该地址会立即生效并可直接使用。
3. **接收消息**：使用生成的地址接收 emails，例如用于在线服务注册、账户验证或测试。消息会实时显示在网站上的 inbox 中。
4. **监控消息**：直接在 Ghostinbox 上访问临时 inbox，查看收到的消息。不需要外部 email 客户端。

![alt text](https://officinebitcoin.it/lezioni/ghostin/email.png)

该服务设计得快速且无摩擦：无需创建账户，极简界面让非技术用户也能顺畅使用。通过 Tor 访问的能力，为希望保持完全匿名的用户增加了一层额外保护。

## 从 alias 到 email
要使用该服务，你需要选择一个足够长且足够随机的 alias，使其他用户无法猜到它。这个 alias 就像访问该 email 的密码，因此不应忘记。

根据这个 alias，会派生出一个 HASH@ghostinbox.it email 地址，其中 HASH 等于 `sha256(alias)`，也就是使用 SHA-256 对 alias 计算得到的 hash；随后用户可以使用这个 email（在接收方案中显示）来接收 emails。接收页面会自动更新并显示收到的 emails。用户可以在不访问服务的情况下创建 email 地址，并仅使用网站进行查看。

点击 email 后，你可以阅读其文本，也可以在需要时复制链接再打开；email 格式被有意设计为纯文本，因此不会显示基于 HTML 的 emails 中的任何图形特性。

## 谁需要 Ghostinbox？
Ghostinbox 满足与 privacy 和临时 email 管理相关的多种需求：

1. **Spam 防护**：使用临时地址，用户可以避免真实 email 地址被 spam 或不想要的 newsletters 淹没。
2. **安全注册**：非常适合注册需要 email 验证的在线服务、论坛或平台，而不会暴露个人 email。
3. **Deliverability 测试**：开发者和营销人员可以使用 Ghostinbox 测试 email 的发送与接收，而无需使用真实地址。
4. **高级 privacy**：得益于 Tor 支持，该服务适合希望在与网站或在线服务交互时保持匿名的用户。
5. **临时使用**：适合需要一次性 email 地址的场景，例如促销、免费试用或短期通信。

![alt text](https://officinebitcoin.it/lezioni/ghostin/stats.png)

## 技术特性
Ghostinbox 的 GitHub repository（https://github.com/valerio-vaccaro/ghostinbox.it）展示了一个轻量级实现，主要使用 Python 和 Flask framework 编写，具有以下特点：

- **Serverless approach**：没有 email 服务器，而是利用免费的 email 和 email forwarding 服务，使服务架构极其简单且经济。
- **架构**：Ghostinbox 使用基于 Flask 的 client-server 架构来管理临时 email 地址的生成和消息显示。设计的简单性确保即使在高请求量下也能保持高性能。
- **地址生成**：临时 email 地址会根据输入的 alias 动态生成。
- **Tor 支持**：该服务被配置为可通过 onion routing 访问，确保用户与网站交互时 IP 地址不会被跟踪。
- **消息管理**：收到的消息会在 30 天后删除。
- **安全性**：个人数据或消息都不会被永久存储。服务设计降低了 breach 风险，而无需注册也消除了提供敏感信息的必要。
- **Open-source**：公开代码允许开发者验证系统完整性、贡献改进，或托管一个定制实例。

技术优势：
- **绝对 privacy**：emails 在 30 天后删除，并且支持 Tor，确保匿名且安全的体验。
- **轻量**：Flask 实现针对低资源占用进行了优化，使服务具备可扩展性并保持快速。
- **透明度**：open-source 许可证允许代码审计和定制，增加用户信任。

## 结论
Ghostinbox 是一个优雅且实用的解决方案，适合寻找快速、安全、以 privacy 为导向的临时 email 服务的用户。凭借直观界面、Tor 支持以及 open-source 代码透明度，它既适合想保护 inbox 免受 spam 影响的普通用户，也适合需要可靠系统进行测试或临时注册的开发者。要试用 Ghostinbox，请访问 https://ghostinbox.it/。要查看代码或为项目做贡献，请参阅 https://github.com/valerio-vaccaro/ghostinbox.it 上的 repository。

