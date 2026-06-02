---
layout: default
title: "通过 Sparrow Wallet airgapped 使用 Jade"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only 课程</span> <span>本项目由 valerio-vaccaro 维护</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# 通过 Sparrow Wallet airgapped 使用 Jade

![alt text](https://officinebitcoin.it/lezioni/jadespa/0.jpg)

得益于 Jade 的 firmware 和硬件特性，可以用它进行完全 airgapped 的通信。

事实上，内置摄像头和显示屏正好承担了向 watch-only wallet 接收和发送消息的功能。

本教程展示如何将 Jade 与 Sparrow Wallet 配合，以 airgapped 方式使用。

整个流程包括先进行设置，然后把 extended public key 从 Jade 导出到 Sparrow watch-only，最后完成一笔 spend transaction。

出于教学安排，本教程决定从 Jade 端开始展示操作顺序。

## 高级设置

选择以 airgapped 方式使用设备，需要进行真正的设置，也就是说必须在 Jade 初始化时完成 (1)，因此 Jade 必须处于未初始化状态。

![alt text](https://officinebitcoin.it/lezioni/jadespa/1.jpg)

屏幕会出现提示，要求从 https://blockstream.com/jade/ 网站查看设置说明。

![alt text](https://officinebitcoin.it/lezioni/jadespa/2.jpg)

Jade 的 airgapped 使用配置只能通过选择 Advanced Setup 来完成。

![alt text](https://officinebitcoin.it/lezioni/jadespa/3.jpg)

Jade 会提示此设置包含一些高级技术功能。只需保持充分注意，然后点击确认按钮。

![alt text](https://officinebitcoin.it/lezioni/jadespa/4.jpg)

为了输入用骰子 entropy 生成的 mnemonic，请选择 Restore Wallet。

![alt text](https://officinebitcoin.it/lezioni/jadespa/5.jpg)

现在必须设置 mnemonic 的长度，可以是 12 或 24 个单词。菜单还提供通过扫描 QR code 来恢复 wallet 的选项：这就是 SeedQr，在专门的 Setup 教程中已经讲过。

![alt text](https://officinebitcoin.it/lezioni/jadespa/6.jpg)

纯粹出于教学和速度原因，本教程展示使用 12 个单词的 mnemonic 进行设置。

下一步必须按说明执行，才能访问 airgapped 功能。实际上，必须选择以 CompactSeedQR 格式导出 recovery phrase，并选择 Yes。

![alt text](https://officinebitcoin.it/lezioni/jadespa/7.jpg)

做出选择后，设备会提醒你必须把 QR code 画在盒中提供的模板上，如 Setup 课程的 "Extra" 部分所示。

![alt text](https://officinebitcoin.it/lezioni/jadespa/8.jpg)

流程结束时，必须继续验证所画内容与设备显示的 CompactSeedQR 是否一致。此时 Jade 的内置摄像头会启用，你必须用它对准刚刚画好的 SeedQR。

![alt text](https://officinebitcoin.it/lezioni/jadespa/9.jpg)

如果图样与设备在刚完成的流程中给出的内容一致，就会显示确认信号。

![alt text](https://officinebitcoin.it/lezioni/jadespa/10.jpg)

现在 Jade 会显示将设备连接到 companion app 的选项：选择 QR。

![alt text](https://officinebitcoin.it/lezioni/jadespa/11.jpg)

下一步同样需要用户做出选择：把 encrypted keys 保存在设备上，或在每次会话时通过扫描刚刚画好的 SeedQR 来加载它们。

![alt text](https://officinebitcoin.it/lezioni/jadespa/12.jpg)

注意：

理解这两种访问选项很有用：

- QR PIN Unlock：初始化期间，Jade 会把 wallet 数据加密保存在设备上；之后始终可以通过 QR PIN 流程解锁 Jade 来访问这些数据。
- SeedQR：每次想把密钥加载到设备上时，都必须由 Jade 扫描 SeedQR。

出于教学安排，在前面的选项中选择了 SeedQR，因此设备将以 stateless 方式使用：Jade 会提示该会话是临时的，设备关机时会 "忘记" 这些密钥。

![alt text](https://officinebitcoin.it/lezioni/jadespa/13.jpg)

导出公钥

现在 Jade 已经专门配置为完全 airgapped 工作，我们进入导出 public key 的敏感阶段。
 
仍然从 Jade 开始，此时它已经回到初始菜单，选择 Options。

![alt text](https://officinebitcoin.it/lezioni/jadespa/14.jpg)

注意：Jade 处于 Temporary Signer 模式，可以从 Active 标识旁边的时钟图标看出。

在 Options 中，选择 Wallet。

![alt text](https://officinebitcoin.it/lezioni/jadespa/15.jpg)

然后选择 Export Xpub。

![alt text](https://officinebitcoin.it/lezioni/jadespa/16.jpg)

此时，Jade 的显示屏会显示一个动态 QR code，它代表 extended public key。在这个子菜单的 Options 中，可以选择导出 multisig/singlesig 以及 derivation path。

本教程选择导出 full segwit singlesig。

![alt text](https://officinebitcoin.it/lezioni/jadespa/17.jpg)

正是在这个阶段，Sparrow 开始发挥作用。启动程序，并通过选择 New Wallet 创建一个新的 wallet。

![alt text](https://officinebitcoin.it/lezioni/jadespa/18.jpg)

为 wallet 命名，然后点击 Create Wallet。

![alt text](https://officinebitcoin.it/lezioni/jadespa/19.jpg)

在下一个设置屏幕中，点击 Airgapped Hardware Wallet。

![alt text](https://officinebitcoin.it/lezioni/jadespa/20.jpg)

Sparrow 会打开一个窗口，显示已实现支持的 hardware wallets。选择 Jade。

![alt text](https://officinebitcoin.it/lezioni/jadespa/21.jpg)

此时，你正在操作的 PC 摄像头会被激活。

![alt text](https://officinebitcoin.it/lezioni/jadespa/22.jpg)

如果有多个 webcam 可用，请在显示 Default Camera 的下拉菜单中选择最合适的一个。

现在拿起 Jade，此时它仍在持续显示代表 Xpub 的动态 QR code，把显示屏放到 PC 摄像头前，并让 QR code 保持在虚线区域内。

![alt text](https://officinebitcoin.it/lezioni/jadespa/23.jpg)

在摄像头画面下方，有一个会变成蓝色的滚动条。

Sparrow 获取 Xpub 的进度就是这样显示的：从 0-100%。

在这个阶段，可能需要做一些调整：增加或降低 Jade 显示屏亮度，以及正面照明，或者在 Sparrow 的下拉菜单中选择 Use HD Capture，或降低分辨率。

不要被这些细节吓到，一旦设置好自己的工作环境，这些阶段就会非常顺手、轻松地完成。 (2)

事实上，当摄像头窗口关闭，并返回 Sparrow 的 Settings 后，所有 watch-only wallet 数据都出现时，就说明导出已经完成。

![alt text](https://officinebitcoin.it/lezioni/jadespa/24.jpg)

按照 Sparrow 的结构，现在需要点击 Apply 来应用 script policy。

wallet 创建会继续进行，需要输入并确认一个用于加密 wallet 文件的密码。

![alt text](https://officinebitcoin.it/lezioni/jadespa/25.jpg)

当右下方的滚动条填满到 100% 时，创建过程就结束了。

![alt text](https://officinebitcoin.it/lezioni/jadespa/26.jpg)

## 花费交易

如果假设 Jade 承担个人 hardware wallet 的角色，就必须假定它持有资金，并且这些资金将来需要被花费。

在选择 Sparrow 作为 watch-only wallet、Jade 作为签名设备之后，我们来看看如何用这两个工具构建、签名并传播一笔交易。

![alt text](https://officinebitcoin.it/lezioni/jadespa/27.jpg)

在示例中，可用总余额为 56,598 sats。

在 Sparrow 左侧菜单中选择 Send，并开始构建 spend transaction。全部设置完成后，点击右下角的 Create transaction。

![alt text](https://officinebitcoin.it/lezioni/jadespa/28.jpg)

会出现一个高级交易窗口，其中可以看到 Sparrow 将 Jade 识别为签名设备 (Signing Wallet)。

如果设置令人满意，点击 Finalize Transaction。

![alt text](https://officinebitcoin.it/lezioni/jadespa/29.jpg)

签名屏幕会出现。在 airgapped 系统中，.psbt 导出通过 QR code 完成，因此在 Sparrow 中点击左下角的 Show QR。

![alt text](https://officinebitcoin.it/lezioni/jadespa/30.jpg)

窗口会显示一个动态 QR code，代表 psbt，接下来需要用 Jade 的摄像头扫描它。

![alt text](https://officinebitcoin.it/lezioni/jadespa/31.jpg)

拿起 Jade，并从主菜单中选择 Scan QR。

![alt text](https://officinebitcoin.it/lezioni/jadespa/32.jpg)

用此时已经激活的 Jade 摄像头对准 Sparrow 正在生成的动态 QR code。hardware wallet 显示屏上的蓝色滚动条会显示读取完成的百分比。

psbt 导入完成后，Jade 会显示交易详情供验证：第一个屏幕显示目标地址和金额，

![alt text](https://officinebitcoin.it/lezioni/jadespa/33.jpg)

第二个屏幕显示费用。在后一个屏幕确认后，Jade 会应用签名。

![alt text](https://officinebitcoin.it/lezioni/jadespa/34.jpg)

Jade 的显示屏会自动显示另一个动态 QR code：这是已签名交易。

在这个屏幕的选项中，可以提高或降低密度，以便与 wallet app 更好地通信。

![alt text](https://officinebitcoin.it/lezioni/jadespa/35.jpg)

与此同时，Sparrow 先前停留在显示动态 QR code 的状态，现在必须设置为接收已签名交易以便传播。

因此，必须点击 Scan QR 来重新激活 PC 的 webcam。

![alt text](https://officinebitcoin.it/lezioni/jadespa/36.jpg)

把 Jade 的显示屏放到 webcam 前，让 Sparrow 导入已签名交易。

![alt text](https://officinebitcoin.it/lezioni/jadespa/37.jpg)

画面下方的滚动条必须完成到 100%，直到导入发生；Sparrow 会如下显示。

![alt text](https://officinebitcoin.it/lezioni/jadespa/38.jpg)

现在再次验证整笔交易；如果没有问题，就可以点击 Broadcast Transaction 进行传播。

在 Transactions 菜单中，会出现这笔转出的交易。

![alt text](https://officinebitcoin.it/lezioni/jadespa/39.png)

注释

- (1) - 如果 Jade 已经初始化，只需进入 Options 菜单 → Settings → Factory reset
- (2) - Jade Original 的显示屏非常小，而且为了把动态 QR code 放入 Sparrow 显示的虚线区域内，需要把显示屏靠近到几厘米的距离。因此，可能需要配备一台分辨率很高且焦距合适的 webcam，或者使用 Iriun 之类的 app，把手机 "变成" PC 的摄像头。事实上，手机在近距离的对焦能力更强。
