---
layout: default
title: "Jade avec Electrum Wallet"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Leçon Bitcoin-only</span> <span>Ce projet est maintenu par valerio-vaccaro</span></p>

## 🌍 Traductions

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Jade avec Electrum Wallet

![alt text](https://officinebitcoin.it/lezioni/jadeele/0_cover.jpg)

Après avoir initialisé Jade, il est possible de commencer à l'utiliser et, pour cela, il faut choisir un wallet de visualisation.

Jade est un dispositif qui peut être utilisé avec plusieurs wallets, ou companion apps comme Blockstream les définit sur son site.

Dans ce tutoriel, nous verrons les étapes d'utilisation, via USB, avec Electrum Wallet.

Prenez le Jade initialisé. Dès qu'il est allumé, il se présente ainsi :


![alt text](https://officinebitcoin.it/lezioni/jadeele/001.jpg)

En sélectionnant Unlock Jade, le menu apparaît et permet de choisir comment connecter le dispositif à la companion app.

Avec Electrum, il est possible de connecter Jade uniquement via USB, il faut donc choisir cette option.

Lancez Electrum, qui s'ouvrira en proposant par défaut l'ouverture du dernier wallet utilisé.

Si c'est la première fois que Jade est connecté à Electrum, sélectionnez Create New Wallet puis Finish.

![alt text](https://officinebitcoin.it/lezioni/jadeele/1.jpg)

Donnez un nom au wallet, par exemple Jade_Officine.

![alt text](https://officinebitcoin.it/lezioni/jadeele/3.jpg)

Sélectionnez Standard Wallet

![alt text](https://officinebitcoin.it/lezioni/jadeele/4.jpg)

Lors du choix du keystore, il est essentiel de sélectionner Use a hardware device.

![alt text](https://officinebitcoin.it/lezioni/jadeele/5.jpg)

Electrum lance la recherche du dispositif hardware

![alt text](https://officinebitcoin.it/lezioni/jadeele/6.jpg)

En connectant l'USB au PC (déjà connecté côté USB C à Jade), le hardware wallet affiche l'écran de verrouillage. Jade se déverrouille en saisissant le PIN à six chiffres défini pendant le setup


![alt text](https://officinebitcoin.it/lezioni/jadeele/7.jpg)

Une fois le dispositif hardware déverrouillé, Electrum détecte Jade. Continuez en cliquant sur Next.

![alt text](https://officinebitcoin.it/lezioni/jadeele/8.jpg)

À ce stade, Electrum demande de définir la script policy ; choisissez Native Segwit.

![alt text](https://officinebitcoin.it/lezioni/jadeele/9.jpg)

La phase de transfert de la clé publique du wallet sur Jade vers Electrum de visualisation commence.

![alt text](https://officinebitcoin.it/lezioni/jadeele/10.jpg)

À la fin de l'exportation de la clé publique, la procédure est terminée.

Le wallet watch-only est prêt et Electrum signale la fin de l'opération avec l'écran suivant.

![alt text](https://officinebitcoin.it/lezioni/jadeele/11.jpg)

Le wallet est effectivement créé et il est possible de commencer à l'explorer : on voit les addresses, les wallet information et, surtout, on peut remarquer en bas à droite l'indication qu'il s'agit d'un wallet créé à partir de Blockstream Jade. Le point vert à côté du logo Blockstream indique que le dispositif est allumé et correctement connecté.

![alt text](https://officinebitcoin.it/lezioni/jadeele/12.jpg)

Transactions de réception et de dépense

Depuis le menu Receive d'Electrum, générez un scriptPubKey (adresse) pour recevoir des fonds. Commencez toujours par un petit montant et faites un test de réception+dépense.

![alt text](https://officinebitcoin.it/lezioni/jadeele/13.jpg)

Une fois les sats reçus, il est possible de vérifier leur arrivée dans le menu History.

![alt text](https://officinebitcoin.it/lezioni/jadeele/14.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeele/15.jpg)

Une fois la transaction confirmée, il est possible de dépenser cet UTXO et de terminer le test.

La dépense nécessitera l'utilisation de Jade pour signer.

Allez dans le menu Send d'Electrum, collez un scriptPubKey et vérifiez-le attentivement.

![alt text](https://officinebitcoin.it/lezioni/jadeele/16.jpg)

Une fois terminé, appuyez sur Pay.

La fenêtre de transaction s'ouvre, dans laquelle il est important de définir les bonnes fees de transaction. Une fois tous les réglages terminés, cliquez sur Preview en bas à droite.

![alt text](https://officinebitcoin.it/lezioni/jadeele/17.jpg)

La fenêtre de transaction affiche plusieurs détails importants, en premier lieu le status : Unsigned.

À ce stade, il est également possible de voir la commande Sign, précisément pour apposer la signature avec Jade.

![alt text](https://officinebitcoin.it/lezioni/jadeele/18.jpg)

Electrum avertit qu'il faut suivre les instructions sur le dispositif hardware, qui est prêt à signer.

Mais avant, il vaut mieux vérifier ce que l'on signe : tous les paramètres de la transaction qui vient d'être définie apparaissent aussi sur Jade, et il est possible de tous les vérifier.

![alt text](https://officinebitcoin.it/lezioni/jadeele/19.jpg)

Pour continuer, assurez-vous de toujours placer le curseur sur la flèche → qui mène aux étapes suivantes, et jamais sur le "X" qui annule l'opération.

L'affichage des vérifications se termine lorsque Jade montre les fees. À ce stade, confirmer revient à apposer la signature.

![alt text](https://officinebitcoin.it/lezioni/jadeele/20.jpg)

Pendant un bref instant, Jade traite la signature.

![alt text](https://officinebitcoin.it/lezioni/jadeele/21.jpg)

Pendant ce temps, dans Electrum, il est possible de constater le status de la transaction, qui est passé de Unsigned à Signed, et il est maintenant possible de propager la transaction en cliquant sur Broadcast.

![alt text](https://officinebitcoin.it/lezioni/jadeele/22.jpg)

Le wallet, ainsi testé, peut être utilisé pour recevoir des UTXO destinés à être conservés en sécurité.

![alt text](https://officinebitcoin.it/lezioni/jadeele/23.jpg)
