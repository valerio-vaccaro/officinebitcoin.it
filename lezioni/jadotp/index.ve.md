---
layout: default
title: "Jade cofà autenticador OTP"
---

# Jade cofà autenticador OTP

Jade la conserva segreti TOTP e la mostra codici temporanei proteti dal PIN. Aggiorna e fa el [setup](../jadeset/index.ve.html), controla data e ora e conserva fora rete i codici de recupero.

Sul servizio seleziona 2FA co app autenticadora. Su Jade sblocada: **Options → Authentication → OTP → New OTP Record**, scansiona el QR (o inserisse URI `otpauth://`), po mete el codice de **View OTP**. No fotografar mai el QR segreto.

I record OTP no i vien restaurai da la seed bitcoin. Prima de perder o resettar Jade fa **Details → Export** e verifica na copia segura. [Guida uficiale](https://help.blockstream.com/blockstream-jade/add-more-security-functionality/use-jade-as-a-2fa-authentication-device).
