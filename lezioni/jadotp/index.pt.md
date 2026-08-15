---
layout: default
title: "Jade como autenticador OTP"
---

# Jade como autenticador OTP

## Introdução, preparação e uso

Jade guarda segredos TOTP e mostra códigos temporários protegidos pelo PIN. Atualize-a e conclua o [setup](../jadeset/index.pt.html); não é necessário programa no computador. Verifique data/hora e guarde offline os códigos de recuperação.

No serviço escolha 2FA por aplicação autenticadora. Na Jade desbloqueada selecione **Options → Authentication → OTP → New OTP Record**, leia o QR (ou URI `otpauth://`), abra **View OTP** e introduza o código no serviço.

No dia a dia escolha o registo em **View OTP**. Nunca fotografe o QR secreto. Registos OTP **não** são recuperados da seed bitcoin: antes de perder ou reiniciar a Jade use **Details → Export** e confirme um backup seguro. Veja a [guia oficial](https://help.blockstream.com/blockstream-jade/add-more-security-functionality/use-jade-as-a-2fa-authentication-device).
