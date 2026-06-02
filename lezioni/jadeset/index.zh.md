---
layout: default
title: "Jade 设置"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only 课程</span> <span>本项目由 valerio-vaccaro 维护</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Jade 设置

![alt text](https://officinebitcoin.it/lezioni/jadeset/0_Cover.jpg)

Jade 到货时带有包装，需要确认包装完好无损，检查位于盒体（下部）和盒盖（上部）之间的两个防拆全息贴纸。

包装内包含一本小型用户手册、两张 CompactSeedQR 模板，以及 hardware wallet。

按住下方按钮即可开启 Jade，随后会显示 3 个菜单：

- Setup Jade
- Scan QR
- Options

你可以在 Options 中按照个人偏好设置多个参数，但首先需要完成初始化。

使用滚动按钮选择 __Setup Jade__ 菜单，并用正面按钮确认。

![alt text](https://officinebitcoin.it/lezioni/jadeset/1.jpg)

屏幕会提示查看网站 https://blockstream.com/jade/ 上的设置说明。

![alt text](https://officinebitcoin.it/lezioni/jadeset/2.jpg)

为了正确执行，建议用掷骰子生成助记词，并用这份熵创建 wallet。因此，选择 __Advanced Setup__。

![alt text](https://officinebitcoin.it/lezioni/jadeset/3.jpg)

Jade 会提示此设置包含一些高级技术功能。只需保持高度注意，并点击确认按钮。

![alt text](https://officinebitcoin.it/lezioni/jadeset/4.jpg)

为了输入用骰子熵生成的助记词，选择 __Restore Wallet__。

![alt text](https://officinebitcoin.it/lezioni/jadeset/5.jpg)

现在必须设置助记词长度，12 个词或 24 个词。菜单还提供通过扫描二维码恢复 wallet 的可能性：这就是 SeedQr，将在其他地方介绍。

![alt text](https://officinebitcoin.it/lezioni/jadeset/6.jpg)

出于纯教学和节省时间的原因，本教程展示使用 12 个词助记词进行设置。

开始输入第一个词的流程后，Jade 会显示键盘，用于输入对应字母。使用滚动按钮，将位置移动到正确的 ← → 位置。

在这个例子中，第 1 个词是 "below"。

![alt text](https://officinebitcoin.it/lezioni/jadeset/7.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/8.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/9.jpg)

输入前 3-4 个字母后，Jade 会从 BIP39 词典中选取单词，并开始给出一系列建议。使用滚动按钮向前或向后移动，直到找到正确的词。

![alt text](https://officinebitcoin.it/lezioni/jadeset/10.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/11.jpg)

继续输入词语，直到到达最后一个词：checksum。

此时，Jade 会显示两种可能性：输入一个已有词，或者使用自身软件计算一个有效的 checksum。

![alt text](https://officinebitcoin.it/lezioni/jadeset/12.jpg)

注意：

- 如果从用掷骰子创建的 12 个词助记词进行设置，建议选择 Existing，并输入该词的前几个字母，从掷骰结果给出的范围中选择。
- 如果设置从用掷骰子生成的 24 个词助记词开始，可以让 Jade 计算所有可能的 checksum，然后选择其中一个。确实会损失一些熵，但只发生在最后一个词上。当你决定把资金托付给 Jade 时，这是可以接受的权衡。
- 如果恢复已有 wallet：选择 Existing 并输入正确的 checksum。

继续使用从掷骰子生成的助记词进行设置的例子，我们在上一菜单中选择 Existing，目的是输入字母并找到对应的 checksum。

![alt text](https://officinebitcoin.it/lezioni/jadeset/13.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/14.jpg)

此时，Jade 会建议以 _CompactSeedQR_ 的形式导出 recovery phrase。

_CompactSeedQR_ 是一种编码方式，它将 mnemonic phrase 转换成二维码，用于在 Jade 上扫描并恢复 wallet。

如果你想尝试这样做，请参见本教程底部的部分，其中解释了具体方法。

![alt text](https://officinebitcoin.it/lezioni/jadeset/15.jpg)

在上一菜单中选择 "No" 后，可以继续完成设置。

设备已准备好连接到它的 watch-only wallet。

下一个菜单显示连接方式：

- USB
- QR code
- Bluetooth

![alt text](https://officinebitcoin.it/lezioni/jadeset/16.jpg)

选择 USB，并用确认按钮确认。

此时，Jade 要求连接到 companion app。

在下面的例子中，选择通过 USB 将设备连接到 Blockstream Green；事实上，这个 wallet 可以检查 Jade 的 firmware 更新，并通过 USB 监听设备，提供引导式设置。

打开 Green，检查网络和安全设置。

如果有 firmware 更新，Green 会立即提示，建议执行升级。

![alt text](https://officinebitcoin.it/lezioni/jadeset/17.jpg)

firmware 更新完成后，Green 开始与 Jade 交互。

此时，签名设备要求设置 duress PIN；它会加密 Jade 上的私钥，使其对任何人都不可访问，只有持有六位 PIN 的人除外。

![alt text](https://officinebitcoin.it/lezioni/jadeset/18.jpg)

当 Green 停留在上方所示屏幕等待时，Jade 上会出现设置 6 位 PIN 的选项，并要求再次正确输入以确认。

![alt text](https://officinebitcoin.it/lezioni/jadeset/19.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/20.jpg)

Jade 会在设备上加密并创建持久数据。

![alt text](https://officinebitcoin.it/lezioni/jadeset/21.jpg)

操作结束后，可能需要等待片刻，Green 会打开已可使用的 wallet。

关闭 Jade 再重新打开后，设备会显示为已初始化，firmware 已更新，并准备解锁（Unlock Jade），以便与其 companion app 配合使用。

![alt text](https://officinebitcoin.it/lezioni/jadeset/22.jpg)

## 附加：创建 CompactSeedQR

在输入助记词结束时，我们跳过了以二维码格式导出密钥的部分，以便专注于设置阶段。这种导出方式以后随时可以完成。

开启 Jade，并从 Options → Temporary Signer → Continue → 12/24 Words 菜单返回 recovery phrase 输入菜单；在该流程结束时，会出现以 SeedQR 格式导出的选择屏幕。

![alt text](https://officinebitcoin.it/lezioni/jadeset/15.jpg)

选择 Yes 后，系统会提醒你必须在盒中提供的模板上绘制二维码。

![alt text](https://officinebitcoin.it/lezioni/jadeset/24.jpg)

流程开始时会显示待绘制二维码的整体预览（出于隐私原因，部分内容已被抹除）。

![alt text](https://officinebitcoin.it/lezioni/jadeset/25.jpg)

随后，网格中的所有格子会逐个显示，根据 recovery phrase 的长度，从 A1 到 C3 或 E5。

![alt text](https://officinebitcoin.it/lezioni/jadeset/26.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/27.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/28.jpg)

画完网格的最后一个格子后，Jade 会再次显示整体预览，以便进行第一次验证。确认 Done 继续。

![alt text](https://officinebitcoin.it/lezioni/jadeset/29.jpg)

Jade 的内置摄像头会启用，你需要用它对准刚刚绘制的 SeedQR。

![alt text](https://officinebitcoin.it/lezioni/jadeset/30.jpg)

如果绘制结果与 Jade 在刚完成的流程中给出的内容一致，就会显示确认信号。

![alt text](https://officinebitcoin.it/lezioni/jadeset/31.jpg)

点击确认 Continue 后，Jade 会从主菜单正常运行。

CompactSeedQR 是在 Jade 上恢复 wallet 的工具。
