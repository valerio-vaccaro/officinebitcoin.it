---
layout: default
title: "Jade OTP-hitelesítőként"
---

# Jade OTP-hitelesítőként

Jade PIN-védetten tárol TOTP titkokat és időalapú kódokat mutat. Frissítsd és végezd el a [beállítást](../jadeset/index.hu.html), ellenőrizd a dátumot/időt, a helyreállító kódokat pedig őrizd offline.

A szolgáltatásnál válaszd az authenticator-app 2FA-t. Feloldott Jade-en: **Options → Authentication → OTP → New OTP Record**, QR beolvasása (vagy `otpauth://` URI), majd a **View OTP** kódját írd be. A titkos QR-t ne fényképezd le.

Az OTP rekordok **nem** állnak vissza bitcoin seedből. Elvesztés vagy reset előtt **Details → Export**, majd biztonságos másolat ellenőrzése. [Hivatalos útmutató](https://help.blockstream.com/blockstream-jade/add-more-security-functionality/use-jade-as-a-2fa-authentication-device).
