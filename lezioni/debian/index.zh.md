---
layout: default
title: "安装 Debian"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only 课程</span> <span>本项目由 valerio-vaccaro 维护</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# 安装 Debian
我们准备一个 USB 驱动器，其中包含从官方网站下载的 Debian 镜像。

我们连接所有线缆（display, keyboard, mouse, and ethernet）。

![alt text](https://officinebitcoin.it/lezioni/debian/1.jpg)

我们连接 USB 安装驱动器。

![alt text](https://officinebitcoin.it/lezioni/debian/2.jpg)

我们打开计算机，并确保装有 Debian 的 USB 驱动器能够启动。

![alt text](https://officinebitcoin.it/lezioni/debian/3.jpg)

## 安装
如果一切正常，Debian 安装程序应该会启动，我们会进入下面的屏幕。

![alt text](https://officinebitcoin.it/lezioni/debian/4.jpg)

我们选择第一行并启动图形化安装。

首先会询问我们的语言；这次安装我会选择 "English"，我觉得它比任何其他翻译都更容易理解。

![alt text](https://officinebitcoin.it/lezioni/debian/5.jpg)

此时会询问我们的地理位置；要找到意大利，需要选择 OTHER->EUROPE->ITALY。

![alt text](https://officinebitcoin.it/lezioni/debian/6.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/7.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/8.jpg)

本地化设置这里我也选择 English。

![alt text](https://officinebitcoin.it/lezioni/debian/9.jpg)

然后我配置意大利语键盘，因为这是我手头可用的键盘。

![alt text](https://officinebitcoin.it/lezioni/debian/10.jpg)

接着我们选择一个用户名，并将域名留空。

![alt text](https://officinebitcoin.it/lezioni/debian/11.jpg)

此时 Debian 会要求你为 root 用户选择一个密码...

![alt text](https://officinebitcoin.it/lezioni/debian/12.jpg)

并创建一个用户及其对应的密码。

![alt text](https://officinebitcoin.it/lezioni/debian/13.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/14.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/15.jpg)

现在我们需要选择安装磁盘；我们将使用整个磁盘，并需要选择要执行安装的磁盘。

![alt text](https://officinebitcoin.it/lezioni/debian/16.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/17.jpg)

然后我们需要选择分区结构；目前我们会把所有内容都放在一个分区中。

![alt text](https://officinebitcoin.it/lezioni/debian/18.jpg)

Debian 提出了一个分区表，但是... 它添加了我们不想要的 swap，所以我们选中它并将其从列表中删除。

![alt text](https://officinebitcoin.it/lezioni/debian/19.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/20.jpg)

现在已经删除它了，我们终于可以写入我们的分区表。

![alt text](https://officinebitcoin.it/lezioni/debian/21.jpg)

Debian 想返回分区表配置，但我们拒绝这个提议。

![alt text](https://officinebitcoin.it/lezioni/debian/22.jpg)

然后我们确认要写入更新后的分区表。

![alt text](https://officinebitcoin.it/lezioni/debian/23.jpg)

现在系统询问我们是否要使用 Debian mirror；我们选择使用。

![alt text](https://officinebitcoin.it/lezioni/debian/24.jpg)

我们选择自己的国家。

![alt text](https://officinebitcoin.it/lezioni/debian/25.jpg)

通常 GARR mirror 很快也很可靠；我们就使用它。

![alt text](https://officinebitcoin.it/lezioni/debian/26.jpg)

我没有任何 proxy，所以将该字段留空。

![alt text](https://officinebitcoin.it/lezioni/debian/27.jpg)

那么要安装哪些程序？由于我们是在制作一台服务器，所以禁用图形环境（取消前两个勾选项），并选择 SSH，因为我们需要它来进行远程访问。

![alt text](https://officinebitcoin.it/lezioni/debian/28.jpg)

安装开始。

最后系统会询问我们是否要安装 grub，它允许我们启动 Linux；我们选择是，并选择安装操作系统的同一块磁盘。

![alt text](https://officinebitcoin.it/lezioni/debian/29.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/30.jpg)

Yuhuuu，完成了；现在可以移除 USB 驱动器，并继续重启机器。

![alt text](https://officinebitcoin.it/lezioni/debian/31.jpg)

如果一切正常，我们应该会看到一个终端，要求我们使用安装过程中创建的某个账户登录。

## 配置

### 开始连接
我们使用 `ssh username@ip` 连接到服务器，其中 username 是安装过程中选择的名称，ip 是我们安装 Debian 的那台计算机的 IP 地址。

当然，如果你是通过显示器和键盘安装，而不是通过网络连接，这一步可以跳过。

请注意，Debian 禁止你使用超级用户凭据（也就是 root）通过 ssh 连接。

### Repository
现在我们来更新 repository。

使用 `su` 命令并输入 root 密码，切换为超级用户。

使用 `nano /etc/apt/sources.list` 命令编辑 repository 文件，并删除其中现有的所有行。

添加以下几行。

```                                                                    
deb http://deb.debian.org/debian/ bookworm contrib main non-free non-free-firmware
# deb-src http://deb.debian.org/debian/ bookworm contrib main non-free non-free-firmware

deb http://deb.debian.org/debian/ bookworm-updates contrib main non-free non-free-firmware
# deb-src http://deb.debian.org/debian/ bookworm-updates contrib main non-free non-free-firmware

deb http://deb.debian.org/debian/ bookworm-proposed-updates contrib main non-free non-free-firmware
# deb-src http://deb.debian.org/debian/ bookworm-proposed-updates contrib main non-free non-free-firmware

deb http://deb.debian.org/debian/ bookworm-backports contrib main non-free non-free-firmware
# deb-src http://deb.debian.org/debian/ bookworm-backports contrib main non-free non-free-firmware

deb http://deb.debian.org/debian-security/ bookworm-security contrib main non-free non-free-firmware
# deb-src http://deb.debian.org/debian-security/ bookworm-security contrib main non-free non-free-firmware

```

然后可以按 `CTRL+x`，再按 `y` 保存文件。

`apt update` 命令可以让我们检查一切是否顺利，并更新软件包列表。

### 更新系统
要更新系统，只需运行以下命令：

- `apt update` 用于更新软件包列表，
- `apt upgrade` 用于更新已安装且存在新版本的软件包。

### 安装 tor 并与 ssh 一起使用
要安装 tor，只需使用命令 `apt install tor`。

安装完成后，可以使用以下命令进行配置：`nano /etc/tor/torrc`。

在文件末尾添加以下几行。

```
HiddenServiceDir /var/lib/tor/hidden_service/
HiddenServicePort 22 127.0.0.1:22
```

然后使用 `systemctl restart tor` 重启 tor；现在可以用 `cat /var/lib/tor/hidden_service/hostname` 找到我们的 onion 地址。

使用 tor 后，我们现在可以从世界任何地方通过 `torify ssh username@onionaddress.onion` 连接到我们的机器。

## 课程安排
Debian 安装是一节会重复进行的课程；下面是已经举行过的列表：

| 日期        | 备注                                           |
|-------------|------------------------------------------------|
| 240415-2200 | 第一节课                                       |
