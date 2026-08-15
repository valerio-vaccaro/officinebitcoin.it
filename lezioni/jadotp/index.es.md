---
layout: default
title: "Jade como autenticador OTP"
---

# Jade como autenticador OTP

## Introducción, preparación y uso

Jade almacena secretos TOTP y muestra códigos temporales protegidos por PIN. Actualízala y completa el [setup](../jadeset/index.es.html); no hace falta software en el ordenador. Comprueba fecha/hora y guarda fuera de línea los códigos de recuperación del servicio.

En el sitio activa 2FA de aplicación autenticadora, sin terminar. En Jade desbloqueada abre **Options → Authentication → OTP → New OTP Record**, escanea el QR (o escribe el URI `otpauth://`), abre **View OTP** y confirma en el sitio con el código.

Para el uso diario selecciona el registro en **View OTP** e introduce el código antes de que caduque. No fotografíes el QR secreto. Los registros OTP **no** se recuperan con la semilla bitcoin: antes de perder o reiniciar Jade usa **Details → Export** y verifica una copia segura. Consulta la [guía oficial](https://help.blockstream.com/blockstream-jade/add-more-security-functionality/use-jade-as-a-2fa-authentication-device).
