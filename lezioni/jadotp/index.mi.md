---
layout: default
title: "Jade come autenticador OTP"
---

# Jade come autenticador OTP

Jade la conserva i segret TOTP e la mostra i codici temporane protett dal PIN. Aggiorna e fa el [setup](../jadeset/index.mi.html), controla data e ora e conserva offline i codici de recuper.

Sul servizio selegiona 2FA con app autenticadora. Su Jade sblocada: **Options → Authentication → OTP → New OTP Record**, scansiona el QR (o inseriss l'URI `otpauth://`), poeu inseriss el codice de **View OTP**. No fotografà mai el QR segret.

I record OTP i se recupera **minga** de la seed bitcoin. Prima de perd o resettà Jade fa **Details → Export** e verifica una copia segura. [Guida ufficial](https://help.blockstream.com/blockstream-jade/add-more-security-functionality/use-jade-as-a-2fa-authentication-device).
