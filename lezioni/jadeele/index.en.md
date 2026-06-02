---
layout: default
title: "Jade with Electrum Wallet"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only lesson</span> <span>This project is maintained by valerio-vaccaro</span></p>

## 🌍 Translations

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Jade with Electrum Wallet

![alt text](https://officinebitcoin.it/lezioni/jadeele/0_cover.jpg)

After initializing Jade, you can start using it and, to do so, you need to choose a viewing wallet.

Jade is a device that can be used with several wallets, or companion apps as Blockstream calls them on its website.

This tutorial shows the steps for using it, via USB, with Electrum Wallet.

Take the initialized Jade. As soon as it is turned on, it looks like this:


![alt text](https://officinebitcoin.it/lezioni/jadeele/001.jpg)

Selecting Unlock Jade opens the menu where you must choose how to connect the device to the companion app.

With Electrum, Jade can only be connected via USB, so that option must be chosen.

Launch Electrum, which will open with the default option of opening the last wallet used.

If this is the first time you connect Jade to Electrum, select Create New Wallet and then Finish.

![alt text](https://officinebitcoin.it/lezioni/jadeele/1.jpg)

Give the wallet a name, for example Jade_Officine.

![alt text](https://officinebitcoin.it/lezioni/jadeele/3.jpg)

Select Standard Wallet

![alt text](https://officinebitcoin.it/lezioni/jadeele/4.jpg)

When choosing the keystore, it is essential to select Use a hardware device.

![alt text](https://officinebitcoin.it/lezioni/jadeele/5.jpg)

Electrum starts scanning for the hardware device

![alt text](https://officinebitcoin.it/lezioni/jadeele/6.jpg)

By connecting the USB to the PC (already connected on the USB C side to Jade), the hardware wallet shows the lock screen. Jade is unlocked by entering the six-digit PIN set during setup


![alt text](https://officinebitcoin.it/lezioni/jadeele/7.jpg)

Once the hardware device is unlocked, Electrum detects Jade. Continue by clicking Next.

![alt text](https://officinebitcoin.it/lezioni/jadeele/8.jpg)

At this point Electrum asks you to set the script policy; choose Native Segwit.

![alt text](https://officinebitcoin.it/lezioni/jadeele/9.jpg)

The transfer of the public key from the wallet on Jade to the Electrum viewing wallet begins.

![alt text](https://officinebitcoin.it/lezioni/jadeele/10.jpg)

At the end of the public key export, the procedure is complete.

The watch-only wallet is ready, and Electrum notifies you that completion was successful with the following screen.

![alt text](https://officinebitcoin.it/lezioni/jadeele/11.jpg)

The wallet has actually been created and you can start exploring it: you can see the addresses, the wallet information and, most importantly, at the bottom right you can notice the indication that it is a wallet created from Blockstream Jade. The green dot next to the Blockstream logo indicates that the device is powered on and connected correctly.

![alt text](https://officinebitcoin.it/lezioni/jadeele/12.jpg)

Receiving and spending transactions

From Electrum's Receive menu, generate a scriptPubKey (address) to receive funds. Always start with a small amount and run a receiving+spending test.

![alt text](https://officinebitcoin.it/lezioni/jadeele/13.jpg)

Once the sats have been received, their arrival can be checked in the History menu.

![alt text](https://officinebitcoin.it/lezioni/jadeele/14.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeele/15.jpg)

Once the transaction has been confirmed, you can spend this UTXO and finish the test.

The spend will require using Jade to sign.

Go to Electrum's Send menu, paste a scriptPubKey and check it carefully.

![alt text](https://officinebitcoin.it/lezioni/jadeele/16.jpg)

When finished, press Pay.

The transaction window opens, where it is important to set the correct transaction fees. Once all settings are complete, click Preview at the bottom right.

![alt text](https://officinebitcoin.it/lezioni/jadeele/17.jpg)

The transaction window shows some important details, first of all the status: Unsigned.

At this stage you can also see the Sign command, precisely to apply the signature with Jade.

![alt text](https://officinebitcoin.it/lezioni/jadeele/18.jpg)

Electrum warns you to follow the instructions on the hardware device, which is ready to sign.

Before doing so, however, it is better to verify what you are signing: all the parameters of the transaction just set also appear on Jade, and you can verify them all.

![alt text](https://officinebitcoin.it/lezioni/jadeele/19.jpg)

To continue, make sure the cursor is always positioned on the arrow → that leads to the next steps, and never on the "X" that cancels the operation.

The verification display ends when Jade shows the fees. At this point, confirming is equivalent to applying the signature.

![alt text](https://officinebitcoin.it/lezioni/jadeele/20.jpg)

For a brief moment Jade processes the signature.

![alt text](https://officinebitcoin.it/lezioni/jadeele/21.jpg)

Meanwhile, on Electrum, you can check the transaction status, which has changed from Unsigned to Signed, and it is now possible to propagate the transaction by clicking Broadcast.

![alt text](https://officinebitcoin.it/lezioni/jadeele/22.jpg)

The wallet, tested in this way, can be used to receive UTXO intended to be stored securely.

![alt text](https://officinebitcoin.it/lezioni/jadeele/23.jpg)
