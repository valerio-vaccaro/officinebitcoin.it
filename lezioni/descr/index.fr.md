---
layout: default
title: "Descripteurs Bitcoin"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Leçon Bitcoin-only</span> <span>Ce projet est maintenu par valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Descripteurs Bitcoin

## Introduction

## Descripteurs
Les descripteurs sont un concept relativement récent et encore peu répandu, mais ils sont utiles pour décrire la structure d'une wallet Bitcoin. Les descripteurs sont des chaînes de caractères lisibles (alphanumériques, hexadécimales et certains symboles comme les parenthèses), conçues pour représenter de manière claire et standardisée une wallet, c'est-à-dire l'ensemble des clés publiques et privées nécessaires pour calculer les soldes, recevoir et dépenser des Bitcoin.

## Évolution de la gestion des wallets
Pour contextualiser les descripteurs, l'intervenant retrace l'évolution des wallets :

- Premières wallets (pre-BIP-32) : aux débuts de Bitcoin Core, les wallets étaient des fichiers contenant des clés générées aléatoirement. Chaque fois que les adresses étaient épuisées, de nouvelles étaient ajoutées, ce qui rendait les sauvegardes fréquentes nécessaires pour éviter de perdre des fonds. Ce système était inefficace.
- BIP-32 (HD Wallet) : avec l'introduction de la génération déterministe hiérarchique, un seed générait une clé maîtresse, dont dérivaient toutes les adresses. Il suffisait de sauvegarder le seed, mais ce n'était pas encore une solution complète.
- Mnémoniques (BIP-39) : par la suite, le seed a été dérivé d'une séquence de 12 ou 24 mots (mnemonic), plus facile à conserver. Toutefois, pour reconstruire une wallet, il fallait aussi connaître les chemins de dérivation (par exemple, Legacy, SegWit) ; sinon les fonds pouvaient devenir irrécupérables.

Le mnemonic seul ne suffit pas, surtout pour les wallets complexes comme les multisig (qui exigent plusieurs signatures) ou celles qui utilisent des scripts avancés (par exemple, timelock ou conditions d'héritage). Certaines wallets essaient toutes les dérivations possibles pour trouver des fonds, tandis que d'autres (par exemple, Electrum) demandent de préciser le type de wallet. En multisig, il faut en outre les clés publiques des autres participants, ce qui complique encore la sauvegarde.

## Que sont les descripteurs et pourquoi sont-ils nécessaires
Les descripteurs sont nés pour surmonter ces limites, en offrant une description complète et flexible de la structure d'une wallet. Ils ne remplacent pas le mnemonic, mais le complètent, en incluant :

- Des clés publiques étendues (xpub, ypub, etc.).
- Des chemins de dérivation (par exemple, m/44'/0'/0' pour Legacy).
- Tous scripts ou conditions de dépense (par exemple, multisig, timelock).

## Exemples pratiques
- Legacy single-sig : un descripteur simple pourrait être `pk([fingerprint/derivation]xpub...)`, où :
1. pk indique une clé publique.
2. [fingerprint/derivation] précise la clé maîtresse et le chemin.
3. xpub génère des adresses (par exemple, 0/* pour la réception, 1/* pour change).
- Multisig : un exemple est `sortedmulti(2, xpub1, xpub2, xpub3)`, qui décrit une wallet 2-of-3 en ordonnant les clés pour assurer la cohérence.
- Scripts complexes : avec des scripts comme p2sh (pay to script hash) ou p2wsh (pay to witness script hash), on peut inclure des conditions avancées, comme timelock ou des combinaisons logiques (and, or).

## Descripteurs et Taproot
Un cas intéressant est le descripteur pour Taproot (tr), qui prend en charge deux modes de dépense :

- Signature directe avec une clé spécifique.
- Un arbre de conditions (par exemple, héritage ou timelock), qui garde la complexité cachée sur la blockchain jusqu'à la dépense.

## Avantages des descripteurs
- Sauvegarde complète : ils contiennent toutes les informations nécessaires pour reconstruire une wallet sans tâtonnement.
- Compatibilité : idéals pour les watch-only wallets, où les fonds sont surveillés sans clés privées.
- Flexibilité : ils prennent en charge single-sig, multisig et les scripts complexes.
- Confidentialité : ils ne révèlent pas de secrets et peuvent être partagés comme un xpub.

## Limites et compatibilité
Toutes les wallets ne prennent pas entièrement en charge les descripteurs. Par exemple, Bitcoin Core n'en implémente qu'un sous-ensemble et exige deux descripteurs séparés pour les adresses et le change. Des logiciels comme Sparrow ou Specter offrent une meilleure prise en charge, permettant l'import/export de descripteurs et la visualisation de leur structure.

Des expériences peuvent être menées avec :
- Sparrow : prend en charge les descripteurs, avec une interface graphique pour les créer ou les analyser.
- BDK : bibliothèque avec interface en ligne de commande pour gérer des descripteurs complexes.
- Testnet/Signet : environnements sûrs pour tester sans risquer de vrais fonds.

## Références

- [BIP-380](https://github.com/bitcoin/bips/blob/master/bip-0380.mediawiki)
- [Bitcoin Improvement Proposal 380](https://github.com/bitcoin/bips/blob/master/bip-0380.mediawiki)
- [Bitcoin Improvement Proposal 380](https://github.com/bitcoin/bips/blob/master/bip-0380.mediawiki)

## Programme
Cette leçon a été créée pour un Satoshi Spritz Connect.
