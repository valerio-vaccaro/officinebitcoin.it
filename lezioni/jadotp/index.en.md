---
layout: default
title: "Jade as an OTP authenticator"
---

# Jade as an OTP authenticator

## Introduction

Jade can store TOTP secrets and display changing one-time codes, like an authenticator app, protected by its PIN. This is useful for email, GitHub, exchanges and other 2FA services.

## Set up Jade and the computer

Update Jade and complete [initial setup](../jadeset/index.en.html). No computer program is required: use a computer or phone only to display the service's 2FA QR code. Check Jade's date and time and save the service recovery codes offline.

## Use it

At the service, choose authenticator-app/TOTP setup but do not finish yet. On an unlocked Jade select **Options → Authentication → OTP → New OTP Record**, scan the QR (or enter the `otpauth://` URI), then open **View OTP** and enter the displayed code at the service.

For daily use open **View OTP**, select the account and type the current code before it expires. Never scan or photograph the secret QR. OTP records are **not** restored from the bitcoin seed: before reset, loss or replacement, use **Details → Export** and verify the backup in a secure second authenticator. See the [official Jade OTP guide](https://help.blockstream.com/blockstream-jade/add-more-security-functionality/use-jade-as-a-2fa-authentication-device).
