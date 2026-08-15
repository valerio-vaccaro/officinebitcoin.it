---
layout: default
title: "Jade comme authentificateur OTP"
---

# Jade comme authentificateur OTP

Jade conserve les secrets TOTP et affiche des codes temporaires protégés par PIN. Mettez-la à jour, finissez le [setup](../jadeset/index.fr.html), vérifiez date/heure et sauvegardez les codes de récupération hors ligne.

Sur le service, choisissez l'application d'authentification. Sur Jade déverrouillée : **Options → Authentication → OTP → New OTP Record**, scannez le QR (ou saisissez l'URI `otpauth://`), puis saisissez le code de **View OTP** sur le site. N'enregistrez jamais le QR secret.

Les enregistrements OTP ne sont **pas** restaurés par la seed bitcoin : avant une perte ou réinitialisation, utilisez **Details → Export** et vérifiez une copie sûre. [Guide officiel](https://help.blockstream.com/blockstream-jade/add-more-security-functionality/use-jade-as-a-2fa-authentication-device).
