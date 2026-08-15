---
layout: default
title: "Jade как OTP-аутентификатор"
---

# Jade как OTP-аутентификатор

Jade хранит секреты TOTP и показывает защищённые PIN одноразовые коды. Обновите Jade, завершите [настройку](../jadeset/index.ru.html), проверьте дату/время и сохраните коды восстановления офлайн.

На сервисе выберите 2FA через приложение. На разблокированной Jade: **Options → Authentication → OTP → New OTP Record**, сканируйте QR (или введите URI `otpauth://`), затем введите код из **View OTP**. Не фотографируйте секретный QR.

Записи OTP **не** восстанавливаются из bitcoin seed. До потери или сброса используйте **Details → Export** и проверьте безопасную копию. [Официальная инструкция](https://help.blockstream.com/blockstream-jade/add-more-security-functionality/use-jade-as-a-2fa-authentication-device).
