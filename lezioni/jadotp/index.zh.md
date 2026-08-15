---
layout: default
title: "将 Jade 用作 OTP 验证器"
---

# 将 Jade 用作 OTP 验证器

Jade 可保存 TOTP 密钥并显示受 PIN 保护的临时验证码。更新设备并完成 [设置](../jadeset/index.zh.html)，检查日期和时间，并离线保存服务提供的恢复代码。

在服务中选择验证器应用 2FA。在已解锁的 Jade 上选择 **Options → Authentication → OTP → New OTP Record**，扫描 QR 码（或输入 `otpauth://` URI），然后在网站输入 **View OTP** 中的代码。切勿拍摄或分享秘密 QR 码。

OTP 记录**不会**从比特币助记词恢复。丢失或重置 Jade 前，请使用 **Details → Export** 并验证安全备份。[官方指南](https://help.blockstream.com/blockstream-jade/add-more-security-functionality/use-jade-as-a-2fa-authentication-device)。
