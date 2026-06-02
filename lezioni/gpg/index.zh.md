---
layout: default
title: "GPG 与 YubiKey 教程"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only 课程</span> <span>本项目由 valerio-vaccaro 维护</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# GPG 与 YubiKey 教程

本课程将引导你使用 Gnu Privacy Guard (GPG)：
- 创建新的密钥对，
- 添加用于签名和加密的子密钥，
- 备份所有密钥，
- 将子密钥转移到 YubiKey，以及
- 使用 Yubikey 加密/签名文件。

本课程面向 Linux，命令已在 GPG 2.2.40/Debian 12 上测试。同样的命令在其他 Linux 版本以及 MacOSX 和 Windows 上也可能以类似方式工作（加密文件系统除外）。

该流程遵循最佳安全实践，例如离线生成密钥和安全备份。

## 安装
安装 gpg 和必要工具

```bash
sudo apt update
sudo apt install gnupg scdaemon pcscd yubikey-manager
```

确认版本为 2.1.17 或更高版本（推荐 2.4.5）。

```bash
gpg --version
```

检查 YubiKey 功能

```bash
ykman info
```

确保 OpenPGP applet 已启用，并且 CCID 模式处于活动状态。

使用隔离网络的机器（无互联网）生成密钥，以防泄露。

请记住，YubiKey 默认 PIN 并不安全，分别是：
- Default User PIN: 123456
- Default Admin PIN: 12345678
使用前请修改它们（见步骤 4）。

## 步骤 1
生成一个仅用于认证 (C) 的主 GPG 密钥对（公钥和私钥）；所有其他密钥都将从它派生。

使用 --expert 启动密钥生成，以访问高级选项。

```bash
gpg --expert --full-gen-key
```

选择密钥类型：

```
Please select what kind of key you want:
   (1) RSA and RSA (default)
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
   (7) DSA (set your own capabilities)
   (8) RSA (set your own capabilities)
   (9) ECC and ECC
  (10) ECC (sign only)
  (11) ECC (set your own capabilities)
  (13) Existing key
  (14) Existing key from card
Your selection? 8
```

选择 (8) RSA (set your own capabilities)，以自定义密钥行为。

设置能力：

```
Possible actions for a RSA key: Sign Certify Encrypt Authenticate 
Current allowed actions: Sign Certify Encrypt 

   (S) Toggle the sign capability
   (E) Toggle the encrypt capability
   (A) Toggle the authenticate capability
   (Q) Finished

Your selection? S
```

禁用 Sign 和 Encrypt（按 S、E）。

保留 Certify（完成后按 Q）。

结果是，在允许的操作中只保留 Certify。

设置密钥大小：

```
RSA keys may be between 1024 and 4096 bits long.
What keysize do you want? (3072) 4096
```

输入 4096（YubiKey 4/5 支持的最大值）。

设置过期时间：

```
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0) 
```

输入 3y（3 年）或你偏好的期限。确认日期。

输入 User ID：

```
GnuPG needs to construct a user ID to identify your key.

Real name: Satoshi Spritz
Email address: info@satoshispritz.it
Comment: 
You selected this USER-ID:
    "Satoshi Spritz <info@satoshispritz.it>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? o
```

提供姓名和电子邮件。评论留空。用 O 确认。

输入强 passphrase（混合字母、数字、符号；避免常见词）。

示例：Tr0ub4dor&3xplor3r!2025

passphrase 用于保护你的私钥。

通过移动鼠标、随机输入，或使用 rng-tools 生成熵（仅 Linux，且只在你充分理解时使用）：

```bash
sudo apt install rng-tools
sudo rngd -r /dev/urandom
```

等待密钥生成完成。从输出中记下 key ID（例如 C2033656849FC82BA3C365E33C9BF8B9CB86875D）：

```
gpublic and secret key created and signed.

pub   rsa2048 2025-07-20 [C]
      C2033656849FC82BA3C365E33C9BF8B9CB86875D
uid                      Satoshi Spritz <info@satoshispritz.it>

```

创建撤销证书，以防密钥被泄露（你的客户端可能已经创建了）：

```bash
gpg --output revoke_master_satoshispritz.asc --gen-revoke C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

选择原因（例如 1 = 密钥已泄露）并保存。

## 步骤 2
创建签名和加密子密钥。将添加两个子密钥，分别用于签名 (S) 和加密 (E)。

主密钥仍然仅用于认证。

编辑密钥：

```bash
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

如有提示，输入 passphrase。

添加签名子密钥：

```
gpg> addkey
Please select what kind of key you want:
   (3) DSA (sign only)
   (4) RSA (sign only)
   (5) Elgamal (encrypt only)
   (6) RSA (encrypt only)
   (7) DSA (set your own capabilities)
   (8) RSA (set your own capabilities)
  (10) ECC (sign only)
  (11) ECC (set your own capabilities)
  (12) ECC (encrypt only)
  (13) Existing key
  (14) Existing key from card
Your selection? 4
```

选择 (4) RSA (sign only)。

设置大小：4096。

设置过期时间：2y（2 年，子密钥可以更频繁轮换）。

确认并输入 passphrase。

添加加密子密钥：

```
gpg> addkey
```

选择 (6) RSA (encrypt only)。

设置大小：4096。

设置过期时间：2y。

确认并输入 passphrase。

保存更改：

```
gpg> save
```

检查子密钥：

```bash
gpg --list-keys --with-subkey-fingerprints C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

示例输出：

```
pub   rsa4096 2025-07-20 [C] [expires: 2028-07-20]
      C2033656849FC82BA3C365E33C9BF8B9CB86875D
uid           [ultimate] Satoshi Spritz <info@satoshispritz.it>
sub   rsa4096 2025-07-20 [S] [expires: 2027-07-20]
      1E3C548D2CA2927D205C1A85426E4AB8E6D72AC3
sub   rsa4096 2025-07-20 [E] [expires: 2027-07-20]
      94C11C615BE049B97899FA3C8DC3736F499D6C3E

```

记下签名 (S) 和加密 (E) 子密钥的 fingerprints。

## 步骤 3
备份所有密钥。为安全起见，将主密钥、子密钥和公钥备份到两个加密 USB 盘。

准备 USB 盘：插入两个 USB 盘（例如 /dev/sdb 和 /dev/sdc）。

创建加密分区（例如使用 LUKS）：

```bash
sudo cryptsetup luksFormat /dev/sdb1
sudo cryptsetup luksOpen /dev/sdb1 backup1
sudo mkfs.ext4 /dev/mapper/backup1
sudo mount /dev/mapper/backup1 /mnt/backup1
```

对 /dev/sdc1 重复操作（例如挂载到 /mnt/backup2）。

导出私钥：导出主密钥和子密钥：

```bash
gpg --armor --export-secret-keys C2033656849FC82BA3C365E33C9BF8B9CB86875D! > /mnt/backup1/secret_master_satoshispritz.asc
gpg --armor --export-secret-keys 1E3C548D2CA2927D205C1A85426E4AB8E6D72AC3! > /mnt/backup2/secret_sign_satoshispritz.asc
gpg --armor --export-secret-keys 94C11C615BE049B97899FA3C8DC3736F499D6C3E! > /mnt/backup2/secret_encrypt_satoshispritz.asc
```

导出公钥：

```bash
gpg --armor --export C2033656849FC82BA3C365E33C9BF8B9CB86875D! > /mnt/backup1/public_master_satoshispritz.asc
gpg --armor --export 1E3C548D2CA2927D205C1A85426E4AB8E6D72AC3! > /mnt/backup2/public_sign_satoshispritz.asc
gpg --armor --export 94C11C615BE049B97899FA3C8DC3736F499D6C3E! > /mnt/backup2/public_encrypt_satoshispritz.asc
```

导出撤销证书：

```bash
cp revoke_master_satoshispritz.asc /mnt/backup1/revoke_master_satoshispritz.asc
cp revoke_master_satoshispritz.asc /mnt/backup2/revoke_master_satoshispritz.asc
```

安全卸载：

```bash
sudo umount /mnt/backup1
sudo cryptsetup luksClose backup1
```

对 backup2 重复。将 USB 盘存放在分开的安全地点（例如保险箱）。

删除本地密钥（可选）：如果使用隔离网络的机器，请删除 GPG 目录：

```bash
rm -rf ~/.gnupg
```

之后需要在将要使用密钥的机器上导入这些密钥。

如果不是隔离网络的机器，请保留密钥，直到转移到 YubiKey。

## 步骤 4
将签名和加密子密钥转移到 YubiKey，同时让主密钥保持离线。

插入 Yubikey 并检查：

```bash
gpg --card-status
```

输出应显示 OpenPGP applet（例如 Version: 2.0）。

修改默认 PIN：

```bash
gpg --change-pin
```

User PIN：设置新的 6-8 位 PIN（例如 654321）。
Admin PIN：设置新的 8 位 PIN（例如 87654321）。

编辑要转移的密钥：

```bash
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

选择并转移签名子密钥：列出密钥以识别子密钥索引：

```
gpg> list
```

示例：

```
sec  rsa4096/3C9BF8B9CB86875D
     created: 2025-07-20  expires: 2028-07-20  usage: C   
     trust: ultimate      validity: ultimate
ssb  rsa4096/426E4AB8E6D72AC3
     created: 2025-07-20  expires: 2027-07-20  usage: S   
ssb  rsa4096/8DC3736F499D6C3E
     created: 2025-07-20  expires: 2027-07-20  usage: E
```

选择签名子密钥：

```
gpg> key 1
```

签名子密钥将带有星号 (*)。

转移到 YubiKey：

```
gpg> keytocard
Please select where to store the key:
   (1) Signature key
   (3) Authentication key
Your selection?
```

输入 Admin PIN（例如 87654321）。签名私有子密钥会转移到 YubiKey，并在 keyring 中由 stub 替代。

选择并转移加密子密钥：取消选择签名子密钥：

```
gpg> key 1
```

选择加密子密钥：

```
gpg> key 2
```

转移到 YubiKey：

```
gpg> keytocard
Please select where to store the key:
   (2) Encryption key
Your selection? 2
```

再次输入 Admin PIN。

保存更改：

```
gpg> save
```

私有子密钥现在位于 YubiKey 上，本地只保留 stubs。

检查 YubiKey：

```bash
gpg --card-status
```

检查 Signature key 和 Encryption key 插槽是否显示子密钥 fingerprints。

导出私有子密钥（用于验证备份）：

```bash
gpg --armor --export-secret-subkeys C2033656849FC82BA3C365E33C9BF8B9CB86875D > secret-subkeys-satoshispritz.asc
```

删除本地 GPG 目录：

```bash
rm -rf ~/.gnupg
```

重新导入公钥和 stubs：

```bash
gpg --import public.asc
gpg --import secret-subkeys-satoshispritz.asc
```

主私钥已不再位于计算机上。

## 步骤 5
使用 YubiKey 为接收者加密并签名一个文件。

准备测试文件：

```bash
echo "This is a secret message." > test.txt
```

获取接收者的公钥（例如 bob@example.com）：

```bash
gpg --keyserver hkps://keys.openpgp.org --search-keys bob@example.com
```

或从文件导入：

```bash
gpg --import bob_public.asc
```

加密并签名：为 bob@example.com 加密，并使用 Yubikey 签名：

```bash
gpg --encrypt --sign --recipient bob@example.com test.txt
```

提示时输入 User PIN（例如 654321）。

如果 YubiKey 需要触摸确认（可选，通过 ykman openpgp keys set-touch 设置），触摸 YubiKey。

输出将是 test.txt.gpg

解密文件（需要 YubiKey）：

```bash
gpg --decrypt test.txt.gpg > test_decrypted.txt
```

输入 User PIN，并在需要时触摸 Yubikey。

检查 test_decrypted.txt 是否与 test.txt 一致。

Bob 可以用他的私钥解密，并验证你的签名：

```bash
gpg --decrypt test.txt.gpg
```

如果你只想签名文件，可以使用以下命令。

```bash
gpg --detach-sign test.txt
```

这会生成名为 test.txt.sig 的输出文件

验证它：

```bash
gpg --verify test.txt.sig test.txt
```

## 安全实践
- 始终在离线机器上生成密钥，以避免暴露。
- 将包含私钥的 USB 盘存放在分开的安全地点（例如保险箱或银行）。
- 使用强且唯一的 PIN。如果 PIN 尝试次数超限（User 为 3 次，Admin 为 3 次），Yubikey 会锁定并需要重置，从而丢失所有密钥。
- 保持 revoke.asc 可访问但安全，以便在密钥被泄露时撤销它。
- 在过期前创建新的子密钥（例如每年一次），如下所示：

```bash
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
gpg> addkey
```

将新的子密钥转移到 YubiKey，并在服务器上更新公钥：

```bash
gpg --keyserver hkps://keys.openpgp.org --send-keys C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

使用第二个 YubiKey 做冗余：

```bash
gpg --import secret.asc
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

对第二个 YubiKey 重复 keytocard 步骤。

如果需要重置 Yubikey：

```bash
ykman openpgp reset
```

从备份恢复子密钥：

```bash
gpg --import secret.asc
```

“Public Key Not Usable”：确保接收者的公钥已导入并受信任：

```bash
gpg --edit-key bob@example.com
gpg> trust
```
设置为 5 = Ultimate trust。
