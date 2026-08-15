---
layout: default
title: "Jade als OTP-Authentifikator"
---

# Jade als OTP-Authentifikator

Jade speichert TOTP-Geheimnisse und zeigt PIN-geschützte Einmalcodes. Aktualisieren Sie Jade, führen Sie das [Setup](../jadeset/index.de.html) aus, prüfen Sie Datum/Uhrzeit und bewahren Sie Wiederherstellungscodes offline auf.

Beim Dienst App-basiertes 2FA wählen. Auf der entsperrten Jade **Options → Authentication → OTP → New OTP Record** wählen, QR (oder `otpauth://`-URI) einlesen und den Code aus **View OTP** auf der Website eingeben. Den geheimen QR nie fotografieren.

OTP-Datensätze werden **nicht** aus der Bitcoin-Seed wiederhergestellt. Vor Verlust oder Reset über **Details → Export** sichern und Kopie testen. [Offizielle Anleitung](https://help.blockstream.com/blockstream-jade/add-more-security-functionality/use-jade-as-a-2fa-authentication-device).
