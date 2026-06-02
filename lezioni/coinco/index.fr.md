---
layout: default
name: "Comprendre le Coin Control manuel"
description: "Guide complet de la sélection manuelle des UTXO. Comprenez pourquoi elle est importante et apprenez à l'utiliser avec plusieurs software wallets (desktop et mobile)"
title: "Comprendre le Coin Control manuel"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Leçon Bitcoin-only</span> <span>Ce projet est maintenu par valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

![cover](https://officinebitcoin.it/lezioni/coinco/cover.webp)

# Comprendre le Coin Control manuel

## Introduction

La robustesse du protocole Bitcoin est garantie par des concepts de base simples. Parmi eux, la transparence se distingue: toutes les transactions Bitcoin sont publiques et facilement vérifiables par n'importe qui. Si cette caractéristique est une pierre angulaire du protocole, parce qu'elle empêche la fraude et garantit l'authenticité des fonds, elle peut aussi poser un défi pour la confidentialité. **Vous êtes-vous déjà demandé si une telle transparence pouvait affecter votre vie privée?**

Vous devriez. Même s'il est assez simple d'accumuler des satoshis non-KYC, votre vie privée est la plus exposée au moment de la dépense.

## Ce qui se passe lorsque vous dépensez un UTXO
Dépenser du Bitcoin ne consiste pas simplement à transférer de la valeur à quelqu'un d'autre.

En consommant l'un de vos UTXOs, vous devez satisfaire les conditions imposées par la transparence du protocole, car vous devez prouver la propriété de ces fonds. Vous devez donc:
- exposer votre clé publique;
- produire une signature numérique.

Le moment de la dépense est donc le plus critique: **dépenser du bitcoin est un acte qui doit être fait consciemment et avec autant de contrôle que possible**.

## Coin Control
Dans le protocole Bitcoin, des éléments comme "compte" ou "unité monétaire" n'existent pas. Le concept d'UTXO n'est pas le sujet principal de cette leçon, mais je vous invite à poser vos questions à votre Satoshi Spritz de confiance ou à demander une leçon ici sur Officine Bitcoin.
Ce que vous devez savoir, c'est qu'avec Bitcoin, ce que vous accumulez puis dépensez sont de petites ou grandes unités comptables mesurées en satoshis, représentées par des `unspent transaction outputs`, les **UTXOs**, aussi appelés `coins`.
Lorsque vous utilisez des UTXOs pour créer une transaction, ils sont entièrement détruits et de nouveaux UTXOs sont créés à leur place.

Les software wallets sont conçus pour faire ce choix automatiquement, en utilisant des coins sélectionnées "au hasard" avec pour seul critère de couvrir le montant à dépenser.

`Coin Control`, aussi appelé `Coin Selection`, est une fonction de certains software wallets qui permet de **sélectionner manuellement les UTXOs à dépenser lors de la construction de votre transaction**.

Supposons que vous ayez une wallet avec 3 UTXOs, respectivement 21,000, 42,000 et 63,000 satoshis.

![img](https://officinebitcoin.it/lezioni/coinco/01.webp)

Si vous devez dépenser 24,000 sats et laissez le software sélectionner automatiquement, une bonne wallet pourrait choisir de combiner UTXO1 + UTXO2 pour payer les 24k sats et les frais de minage, en créant une monnaie qui revient à une adresse interne de la wallet d'origine.

![img](https://officinebitcoin.it/lezioni/coinco/02.webp)

Après la transaction, la nouvelle situation dans la wallet, en comptant seulement les UTXOs, peut se résumer ainsi.

![img](https://officinebitcoin.it/lezioni/coinco/03.webp)

Avec le bon software et votre vigilance, vous auriez cependant pu faire un choix différent et plus correct. Par exemple, en sélectionnant uniquement UTXO2 (42,000 sats).

![img](https://officinebitcoin.it/lezioni/coinco/04.webp)

Avec une situation finale des UTXOs dans votre wallet qui se présente différemment.

![img](https://officinebitcoin.it/lezioni/coinco/05.webp)

## Pourquoi sélectionner manuellement les UTXOs?
![img](https://officinebitcoin.it/lezioni/coinco/06.webp)

Dans notre exemple, le solde est en réalité le même: `108,280 sats`. Après avoir dépensé 24,000 sats, sans coin control nous aurions 2 UTXOs dans la wallet; avec le coin control manuel, nous en avons 3 au total.

**Pourquoi faire tout cela?**

Il existe, ou il pourrait exister, plusieurs raisons pour lesquelles nous n'avons pas utilisé `UTXO1` **et elles sont toutes à la base de la raison pour laquelle - au moment de dépenser - activer le coin control manuel est une bonne pratique à suivre**.

## Vie privée
Le principal avantage, lorsque l'on parle de sélection manuelle des coins, est **une meilleure confidentialité pour celui qui dépense**.

Reprenons notre exemple: dépenser 24,000 satoshis _sans coin control_. Puisque la blockchain Bitcoin est un registre public, un observateur externe peut affirmer, sans aucun doute, que les inputs `UTXO1 of 21,000 sats` et `UTXO2 of 42,000 sats`, ainsi que la monnaie, `UTXO5 of 38,280 sats`, **appartiennent tous au même utilisateur**.

En sélectionnant manuellement `UTXO2`, au contraire, `UTXO1` reste complètement privé, dans l'UTXO set, en attendant d'être dépensé à un moment plus approprié.

`UTXO1` pourrait provenir d'une source KYC, par exemple un paiement reçu pour des biens et services, tandis que les autres UTXOs non.

**Si c'était votre wallet, voudriez-vous qu'un observateur externe puisse retracer votre identité avec une telle certitude?** Les wallets qui implémentent la sélection manuelle des UTXO permettent, par exemple, la **ségrégation d'un ou plusieurs UTXOs**, une fonction à utiliser lorsque de telles situations se présentent.

Même si je pense que les fonds KYC devraient être conservés dans une wallet séparée des bitcoin non-KYC, si c'est votre cas, ségréger certaines de vos adresses est une aide fondamentale, que vous pouvez obtenir en apprenant à sélectionner manuellement vos inputs de dépense.

## Économie de frais
Sélectionner le bon UTXO pour une dépense permet d'optimiser les frais. Là encore, dans notre exemple, la software wallet a sélectionné deux UTXOs pour couvrir la dépense. Deux UTXOs signifient deux signatures à montrer au réseau, donc un poids de transaction plus élevé en termes de vBytes.

Avec le coin control manuel, vous pouvez n'en sélectionner qu'un seul, suffisant pour couvrir le montant, et économiser des frais parce que le "poids" de la transaction diminue.

Lorsque les frais sont élevés, mais que vous êtes obligé de dépenser du bitcoin on-chain (par exemple pour ouvrir un canal Lightning Network), le coin control devient la bonne incitation économique à utiliser.

## Agrégation de la monnaie
Lors d'un paiement avec Bitcoin on-chain, la possibilité de recevoir de la monnaie devient presque toujours une certitude. Chaque monnaie est en elle-même une petite perte de confidentialité, car elle révèle au réseau l'une de vos adresses qui peut être associée à votre input d'origine.

Étant donné que les meilleures HD wallets génèrent des adresses spéciales pour la monnaie, vous pouvez facilement les reconnaître et "ségréger" toute la monnaie issue de différentes transactions; lorsqu'elle atteint un certain montant, vous pouvez la sélectionner et la consolider manuellement, ou l'échanger sur Lightning Network (ma méthode préférée) pour récupérer la confidentialité perdue lors de la dépense.

## Dépenser depuis une cold wallet
Une cold wallet est un outil avec lequel vous pouvez raisonnablement atteindre un bon niveau de sécurité, afin de stocker toute quantité de fonds à conserver de côté pendant longtemps. Toutefois, des imprévus peuvent survenir et vous obliger à accéder à votre épargne pour couvrir des dépenses inattendues.

Mon conseil est de **ne jamais dépenser directement depuis la cold wallet, afin d'éviter de recevoir la monnaie parmi les adresses de cette même wallet**. Apprenez à sélectionner manuellement les UTXOs nécessaires pour couvrir la dépense, transférez-les vers une hot wallet et préparez votre transaction depuis celle-ci. Toute monnaie, ensuite, peut être renvoyée vers une adresse de cold wallet (si le montant est approprié), ou utilisée à d'autres fins.

## Démonstration pratique
Après cette longue introduction, voyons comment mettre coin control en pratique avec différents software desktop et mobile. Nous utiliserons toujours la même HD wallet, importée dans chacun des outils choisis, pour vous montrer les petites différences entre eux.

## Desktop Wallets

## Sparrow
Si vous utilisez Sparrow, ouvrez votre wallet et sélectionnez _UTXOs_ dans le menu de gauche. Vous verrez la liste de tous les UTXOs associés à votre wallet.

Cliquez simplement sur l'un d'eux, puis choisissez _Send Selected_. Sparrow vous montre aussi le total sélectionné pour la dépense, à côté de la commande.

![img](https://officinebitcoin.it/lezioni/coinco/07.webp)

Vous pouvez aussi en sélectionner plusieurs. Utilisez la touche _CTRL_ pour sélectionner des UTXOs non adjacents dans la liste.

![img](https://officinebitcoin.it/lezioni/coinco/08.webp)

Après avoir sélectionné manuellement les UTXOs, Sparrow vous montrera clairement, graphiquement, comment votre transaction est construite, et vous pourrez la finaliser et la compléter.

![img](https://officinebitcoin.it/lezioni/coinco/09.webp)

### Ségrégation d'UTXO
Ségréger des fonds signifie les "verrouiller" dans la wallet afin qu'ils ne puissent pas être utilisés comme inputs de transaction.

Sparrow permet cette fonction, accessible depuis le menu _UTXOs_. Survolez l'UTXO à "verrouiller" et faites un clic droit. Parmi les options, vous trouverez _Freeze_. Voilà comment vous pouvez ségréger un UTXO avec Sparrow Wallet.

![img](https://officinebitcoin.it/lezioni/coinco/29.webp)

## Electrum
Si votre desktop wallet est Electrum, vous pouvez sélectionner manuellement des UTXOs depuis les menus _Addresses_ et _Coins_.
Dans les deux menus, la sélection se fait en pointant la souris sur l'UTXO et en choisissant _Add to coin control_ après un clic droit.

![img](https://officinebitcoin.it/lezioni/coinco/10.webp)

Vous pouvez aussi sélectionner plus d'un UTXO, avec la touche _CTRL_ s'ils ne sont pas adjacents.

![img](https://officinebitcoin.it/lezioni/coinco/11.webp)

Electrum mettra graphiquement en évidence les UTXOs sélectionnés en vert et, en bas, une barre de la même couleur montre le solde disponible après coin control.

![img](https://officinebitcoin.it/lezioni/coinco/12.webp)

Une fois les output(s) sélectionnés, vous pouvez construire votre transaction comme d'habitude depuis le menu _Send_.

### Ségrégation d'UTXO
Electrum fournit cette option dans le menu _Coins_ en sélectionnant un UTXO précis puis en choisissant _Freeze_ avec le bouton droit de la souris. Vous pouvez aussi "geler" une adresse sans fonds depuis le menu _Addresses_, ou la "coin", pour empêcher la dépense.

![img](https://officinebitcoin.it/lezioni/coinco/28.webp)

## Nunchuk
Nunchuk vous permet de sélectionner des UTXOs depuis le menu principal une fois ouvert.
Lancez Nunchuk et cliquez sur _View coins_.

![img](https://officinebitcoin.it/lezioni/coinco/13.webp)

Une fenêtre s'ouvre avec tous les UTXOs de votre wallet, où vous pouvez en sélectionner un ou plusieurs en cochant la case à côté de chaque montant. Après la sélection, continuez avec _Create transaction_.

![img](https://officinebitcoin.it/lezioni/coinco/14.webp)

Vous pouvez ensuite saisir l'adresse de destination, définir le montant et les frais.

![img](https://officinebitcoin.it/lezioni/coinco/15.webp)

## Blockstream App
Blockstream App desktop, anciennement connue sous le nom de Green, permet la sélection des coins une fois que vous avez commencé à construire la transaction. Ouvrez votre wallet et cliquez sur _Send_.

![img](https://officinebitcoin.it/lezioni/coinco/16.webp)

Collez l'adresse de destination dans le champ approprié, puis sélectionnez _Manual coin selection_.
![img](https://officinebitcoin.it/lezioni/coinco/17.webp)
Une fenêtre s'ouvre où vous pouvez sélectionner un ou plusieurs UTXOs. Dans l'exemple suivant, nous avons sélectionné deux coins. Confirmez ensuite le choix en cliquant sur _Confirm Coin Selection_.

![img](https://officinebitcoin.it/lezioni/coinco/18.webp)

Définissez le montant et les frais, puis poursuivez votre transaction comme d'habitude.

![img](https://officinebitcoin.it/lezioni/coinco/19.webp)

⚠️ Note: Dans le menu _Coins_ de Green, il existe des options _Lock_/_Unlock_ qui suggèrent la possibilité de ségréger des UTXOs. Cela n'est disponible que dans les comptes dits multisig; la fonction ne s'active que pour de très petits UTXOs, proches du seuil `Dust`.

## Mobile Wallets

## Blue Wallet
Même sur mobile, vous pouvez choisir des wallets qui permettent la sélection manuelle des UTXO. Regardons d'abord Blue Wallet.

Si vous utilisez ce software, ouvrez votre wallet et cliquez pour entrer dans les écrans de commande de l'une de vos wallets. Pour accéder au coin control, vous devez entrer dans la phase de dépense, donc cliquez sur _Send_.

![img](https://officinebitcoin.it/lezioni/coinco/21.webp)

Sur l'écran suivant, choisissez le menu indiqué par les trois points en haut à droite. Une fenêtre déroulante avec plusieurs commandes s'ouvre. Choisissez la dernière: _Coin Control_.

![img](https://officinebitcoin.it/lezioni/coinco/22.webp)

À ce stade, Blue Wallet affiche tous vos UTXOs. En plus des montants, ils sont différenciés graphiquement par des couleurs différentes.

![img](https://officinebitcoin.it/lezioni/coinco/27.webp)

Sélectionnez l'UTXO, puis sélectionnez _Use Coin_.

![img](https://officinebitcoin.it/lezioni/coinco/23.webp)

Blue Wallet vous ramène à la fenêtre _Send_ pour continuer à construire la transaction. Ajustez le montant et les frais, puis choisissez _Next_.

![img](https://officinebitcoin.it/lezioni/coinco/24.webp)

Vous pouvez maintenant compléter la transaction comme d'habitude.

### Ségrégation d'UTXO
Blue Wallet permet aussi de ségréger des UTXOs, en les rendant indisponibles pour la dépense, ce qui est une bonne fonction pour une mobile wallet.

Accédez au coin control comme expliqué ci-dessus et, après avoir sélectionné l'UTXO, choisissez _Freeze_ au lieu de _Use Coin_.

![img](https://officinebitcoin.it/lezioni/coinco/26.webp)

## Nunchuk
La version mobile de Nunchuk permet aussi aux utilisateurs d'effectuer du coin control. Si vous utilisez cette app sur mobile, ouvrez-la et allez dans le menu _Wallet_. De là, choisissez _View coins_.

![img](https://officinebitcoin.it/lezioni/coinco/30.webp)

Dans la fenêtre avec la liste des UTXOs, cliquez sur _Select_.

![img](https://officinebitcoin.it/lezioni/coinco/38.webp)

À côté de chaque UTXO, la fonction de sélection apparaît. Comme dans la version desktop, sur Nunchuk mobile, la sélection manuelle se fait en cochant la case à côté du montant. L'écran affiche le nombre d'UTXOs sélectionnés et le montant total disponible. Une fois terminé, le symbole ₿ en bas à gauche est la commande pour commencer à construire la transaction.

![img](https://officinebitcoin.it/lezioni/coinco/31.webp)

Vous pouvez maintenant compléter la transaction, en choisissant le montant et en cliquant sur _Continue_.

![img](https://officinebitcoin.it/lezioni/coinco/32.webp)

Continuez comme d'habitude, en collant une adresse de destination, une description et en personnalisant les réglages des frais.

## Bitcoin Keeper
Bitcoin Keeper est la dernière wallet que nous verrons dans ce guide. Regardons sa fonction de coin control avec une wallet single-sig, même si cet usage n'est pas l'objectif principal de cette app particulière.

Après avoir configuré Keeper sur votre téléphone, lancez-la et ouvrez une wallet contenant quelques UTXOs. Au centre de l'écran principal, cliquez sur _View All Coins_.

![img](https://officinebitcoin.it/lezioni/coinco/34.webp)

Keeper affiche une vue d'ensemble des UTXOs. Pour accéder à l'écran de sélection, cliquez sur _Select To Control_.

![img](https://officinebitcoin.it/lezioni/coinco/35.webp)

Vous pouvez sélectionner des coins en les cochant, puis en cliquant sur la commande appropriée. Une fois terminé, cliquez sur _Send_.

![img](https://officinebitcoin.it/lezioni/coinco/36.webp)

Bitcoin Keeper vous amène directement au menu _Send_, où vous pouvez construire la transaction avec les UTXOs sélectionnés.

![img](https://officinebitcoin.it/lezioni/coinco/37.webp)

## Hardware wallet
Chacune des software wallets vues dans ce guide peut être l'interface watch-only de votre hardware wallet. Cela signifie que le coin control pour un appareil de signature offline se fait avec les étapes vues jusqu'ici.

## Recommandations générales
Coin control est une pratique très efficace pour sélectionner vos inputs de transaction. La sélection manuelle est encore plus efficace si, lorsque vous recevez vos fonds, vous avez bien étiqueté l'origine de vos satoshis. Si vous voulez maîtriser cette technique, je recommande le tutoriel:

https://planb.network/tutorials/privacy/on-chain/utxo-labelling-d997f80f-8a96-45b5-8a4e-a3e1b7788c52
