---
layout: default
title: "Signatures numériques"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Leçon Bitcoin-only</span> <span>Ce projet est maintenu par valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Signatures numériques
Le sujet de cette leçon sera les signatures numériques et leur application à Bitcoin.

## Qu'est-ce qu'une signature ?
Nous devons comprendre ce que nous entendons par signature numérique. Quand nous pensons à une signature normale, nous pensons généralement à autre chose : puisqu'il s'agit de documents numériques, la signature numérique lie à la fois l'identité de l'auteur et l'état du document signé ; en substance, la signature dépend donc aussi du document que nous allons signer.

C'est une très grande différence avec le monde physique, où nous apposons la signature presque sans nous soucier du support sur lequel nous le faisons. Bien sûr, nous n'irions peut-être pas signer des chèques ou d'autres documents sans nous en préoccuper, mais, en substance, la signature que nous apposons ne varie pas.

Les signatures numériques sont quelque chose d'un peu différent ; elles reposent normalement sur des algorithmes à clé publique et clé privée. Cela signifie que quelque part dans le monde, notre wallet possède une paire de clés, publique et privée, et que notre (pseudo-)identité est liée à la clé publique que tout le monde connaît ou que nous ferons connaître à tout le monde.

Nous utiliserons notre clé privée, qui est un nombre, et avec un peu de magie mathématique nous produirons une signature qui est un autre nombre, différent, et qui prouve qu'un certain état d'un certain document appartient à, ou est connu par, une certaine identité liée à une clé publique. Ce que je vais signer est l'empreinte (ou HASH) d'un certain document (ou PAYLOAD).

J'ai aussi besoin d'un générateur de nombres aléatoires ; je mets toutes ces données dans une "boîte noire" qui produit une signature pour moi. La signature prouve donc la possession parce que je signe avec mon secret, mais elle prouve aussi que ce que je signe n'a pas été modifié.

Si je modifie le PAYLOAD, je modifie le HASH et, évidemment, cela invalide la signature.

Pourquoi donc cette signature plus complexe a-t-elle été introduite dans le monde numérique ? Parce que dans le monde numérique, contrairement au monde physique (et peut-être que ceux qui ont séché les cours s'en souviennent), copier une signature est beaucoup plus simple.

La signature numérique contient au contraire des informations sur le document ; elle change donc pour chaque document et ne peut pas être collée puis réutilisée sur un document différent.

La signature numérique sert donc à :
- prouver que j'ai créé un certain message, que je demande une certaine action ou que je déclare un certain état d'un système, et
- prouver que ce message, ce document ou cette chaîne de données n'a pas été manipulé, c'est-à-dire qu'il s'agit bien de ce que je voulais signer.
- rendre une certaine action non répudiable ; si j'ai produit une signature, c'est bien moi qui l'ai fait pour ce document précis.

## Signatures dans Bitcoin
Cette technologie est utilisée dans Bitcoin sous l'acronyme ECDSA (Elliptic Curve Digital Signature Algorithm), un algorithme permettant de produire des signatures numériques sur des courbes elliptiques ; pour l'instant, nous ne traiterons pas d'autres schémas de signature.

Rappelons que dans Bitcoin, on peut produire des signatures pour :
- du texte arbitraire, peu important et peu utilisé
- de nouvelles transactions, dans le but d'autoriser la dépense d'un certain UTXO

Mais comment ces signatures se lient-elles à la transaction ? Chaque adresse possède un mécanisme de dépense, des scripts qui doivent être exécutés pour savoir si une dépense peut être autorisée. Dans ces scripts se trouvent des commandes (ou OPCODES) destinées à vérifier les signatures numériques, comme OP_CHECKSIG, OP_CHECKSIGVERIFY, OP_CHECKMULTISIG, OP_CHECKMULTISIGVERIFY

Rappelons qu'une transaction Bitcoin se compose de :
- Inputs, c'est-à-dire les fonds que je vais dépenser et pour lesquels je dois produire un script de dépense
- Outputs, c'est-à-dire les nouvelles adresses vers lesquelles les fonds iront (et à chaque adresse est associé un mode de dépense bien défini.

En substance, dans la plupart des cas, je devrai donc produire POUR CHAQUE INPUT la ou les signatures nécessaires pour compléter le script de dépense.

Rappelons que cette action nous permet de prouver que cet input est à nous et que nous voulons le dépenser (nous voulons transférer entièrement la propriété, la diviser ou la joindre à d'autres inputs).

Évidemment, la transaction est valide si tous les inputs sont correctement signés ; si ne serait-ce qu'un seul input n'est pas signé, cette transaction ne peut pas être considérée comme valide.

La signature est vérifiable par tous et non répudiable, mais, pour la flexibilité, Satoshi a très habilement introduit plusieurs modes de signature : la signature reste toujours la même, mais le PAYLOAD change, c'est-à-dire la portion de transaction qui fait l'objet de la signature. Cela permet, par exemple, de générer des schémas et des protocoles complexes dans lesquels des morceaux de transactions peuvent être combinés entre eux ; Satoshi a appelé ces modes (de véritables flags dans le langage de scripting) SIGHASH.

## SIGHASH
Le SIGHASH le plus simple est SIGHASH_ALL, qui signifie générer une signature avec TOUS LES INPUTS et TOUS LES OUTPUTS ; c'est le mode le plus simple et le plus utilisé pour faire une signature.

Une première différence apparaît avec SIGHASH_NONE, qui signe TOUS LES INPUTS, mais AUCUN des OUTPUTS, ce qui permet d'ajouter des outputs ou de modifier les fees ensuite. ATTENTION : avec ce schéma, s'il n'est pas protégé par multisig ou par d'autres fonctionnalités, un miner ou toute personne qui voit une transaction avec ce schéma de signature peut remplacer les outputs en redirigeant les fonds vers sa propre adresse.

Un flag plus intéressant est SIGHASH_SINGLE, dans lequel une paire input-output est signée à condition qu'elle soit insérée dans une transaction au même niveau (par exemple, cinquième input et cinquième output) ; cela permettrait de composer des transactions plus grandes à partir de ces paires, mais ne donne pas la possibilité d'introduire de la monnaie rendue, c'est-à-dire que cela exige la dépense totale de l'input.

En parallèle, tous ces SIGHASH peuvent être combinés avec le flag ANYONECANPAY, qui limite la signature uniquement à l'input pour lequel elle est produite, donnant ainsi à n'importe qui la possibilité d'ajouter des inputs à la transaction.

Toutes ces signatures sont valides quel que soit le type d'adresse et de scripts, laissant au wallet une flexibilité maximale d'expression. Celui-ci utilisera normalement SIGHASH_ALL, mais pourrait aussi suivre des protocoles plus complexes exigeant des schémas de signature différents. En cas de multisig, il n'est pas nécessaire d'utiliser le même type de signature ; un wallet 2-of-2 pourrait signer certains de ses UTXO avec SIGHASH_NONE et ANYONECANPAY afin de donner le contrôle complet au second signataire, qui pourrait par exemple collecter tous ces inputs dans une transaction à signer avec SIGHASH_ALL.

## Signatures sur du texte arbitraire
Par souci d'exhaustivité, les mêmes signatures utilisées pour les inputs de transactions peuvent aussi être utilisées pour signer du texte arbitraire.

Bitcoin propose un schéma dans lequel du texte est ajouté pour empêcher que cette fonctionnalité soit utilisée afin de signer des parties de transactions ; ainsi, si vous avez Bitcoin Core ou même certains wallets, vous pouvez chercher une fonctionnalité de signature de message texte basée sur l'une de vos adresses.

Le wallet utilisera la clé privée associée à la clé publique qui a généré cette adresse pour produire des signatures de messages texte.

Au moment de la vérification, la clé publique est obtenue et peut ensuite être utilisée pour régénérer l'adresse ; donc, si j'ai le texte et la signature, j'extrais la clé publique qui l'a signé, puis à partir de cette clé publique je peux recalculer l'adresse et la vérifier, par exemple, avec celle qui a été fournie.

## Programme
La leçon sur les signatures peut être répétée ; voici la liste de celles déjà tenues :

| Date        | Notes                                          |
|-------------|------------------------------------------------|
|||
