---
layout: default
title: "Mnemonics & Dice : apprendre à créer votre mnémonique"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Leçon Bitcoin-only</span> <span>Ce projet est maintenu par valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Mnemonics & Dice : apprendre à créer votre mnémonique

## Introduction
Créer la mnémonique en utilisant votre propre source d'entropie réduit la surface d'attaque d'un portefeuille Bitcoin ; cependant, certains facteurs doivent être pris en compte :

- le processus doit être aussi simple et rapide que possible, sans fioritures ni répétitions inutiles,
- l'entropie ne doit pas être copiée sur des appareils inutiles et la nécessité d'effectuer des calculs ou des traitements doit être réduite au minimum,
- l'utilisation de logiciels/scripts/programmes doit être évitée, sauf si vous avez effectué une revue précise du code et de toutes les dépendances,
- des configurations différentes peuvent nécessiter des processus légèrement différents.

## Création des mots
La première étape consiste à calculer les 12 ou 24 mots de la mnémonique ; 12 mots sont normalement plus que suffisants pour la sécurité d'un portefeuille Bitcoin.

Pour la génération des mots, vous pouvez utiliser la méthode décrite dans [TRGM](https://github.com/valerio-vaccaro/TRMG), avec 3 dés dont 1 à 8 faces et 2 à 16 faces. CHAQUE lancer de dés correspond à UN SEUL ET UNIQUE mot ; pour le trouver, il suffit de parcourir le tableau du site en cherchant la correspondance des dés avec le lancer effectué (le premier dé est TOUJOURS celui à 8 faces). La colonne du mot contient le mot que vous cherchez.

La recommandation est de générer les 12 ou 24 mots et, si nécessaire, de corriger le dernier ou, dans tous les cas, d'utiliser les dés pour générer l'entropie relative au dernier mot.

## Calcul du checksum
Le dernier mot n'est pas entièrement décidé par nous, mais contient une partie de contrôle ; autrement dit, nous ne pouvons pas choisir intégralement les 11 bits d'entropie qui le composent. Nous pouvons en revanche choisir les 7 premiers dans le cas d'une mnémonique de 12 mots ou les 3 premiers dans le cas d'une mnémonique de 24 mots.

Supposons que notre dernier mot soit BACON, correspondant aux lancers 1, 9 et 11 (rappelez-vous que le premier dé est TOUJOURS celui à 8 faces). Le tableau indique aussi Group 12 et Group 24, qui nous permettent de regrouper les mots en considérant uniquement l'entropie des deux premiers lancers (group 12) ou uniquement celle du premier lancer (group 24).

Supposons que nous voulions construire une mnémonique de 12 mots ; cela signifie que le checksum sera un mot parmi les 16 possibles ayant le même group 12 que bacon, c'est-à-dire 0001000. Les mots possibles sont :

|First|Second|Third|Index|Word	|Index in binary|Group 12	|Group 24|
|---|---|---|-------|-----------|---------------|-----------|---|
|1  |9	|1	|128	|avoid	    |00010000000	|0001000	|000|
|1  |9	|2	|129	|awake	    |00010000001	|0001000	|000|
|1  |9	|3	|130	|aware	    |00010000010	|0001000	|000|
|1  |9	|4	|131	|away	    |00010000011	|0001000	|000|
|1  |9	|5	|132	|awesome	|00010000100	|0001000	|000|
|1  |9	|6	|133	|awful	    |00010000101	|0001000	|000|
|1  |9	|7	|134	|awkward	|00010000110	|0001000	|000|
|1  |9	|8	|135	|axis	    |00010000111	|0001000	|000|
|1  |9	|9	|136	|baby	    |00010001000	|0001000	|000|
|1  |9	|10	|137	|bachelor	|00010001001	|0001000	|000|
|1  |9	|11	|138	|bacon	    |00010001010	|0001000	|000|
|1  |9	|12	|139	|badge	    |00010001011	|0001000	|000|
|1  |9	|13	|140	|bag    	|00010001100	|0001000	|000|
|1  |9	|14	|141	|balance	|00010001101	|0001000	|000|
|1  |9	|15	|142	|balcony	|00010001110	|0001000	|000|
|1  |9	|16	|143	|ball   	|00010001111	|0001000	|000|

Comment trouver le seul mot correct parmi les différentes possibilités ? Cela dépend de votre configuration ; voyons quelques exemples :

- bruteforce, c'est-à-dire les essayer tous dans l'ordre jusqu'à trouver le bon (très laborieux avec des mnémoniques de 24 mots) ; c'est la méthode à utiliser avec Ledger ou avec Electrum (en veillant à sélectionner l'option BIP39),
- calculer tous les mots possibles avec les 11 ou 23 premiers mots et chercher le seul qui appartient à cet ensemble ; cette méthode est utilisable avec Jade et avec d'autres hardware wallets capables de calculer tous les mots finaux possibles d'une mnémonique,
- saisir la mnémonique complète et laisser le hardware wallet la corriger pour nous, comme le fait Specter-DIY de manière très élégante, par exemple.

## Backup (sujet d'une autre leçon)
Il est fondamental d'avoir une bonne politique de backup, donc :
- plusieurs backups,
- sur plusieurs supports et
- éventuellement chiffrés ou divisés (mais il faut savoir le faire correctement).

## Bibliographie

- [TRMG](https://github.com/valerio-vaccaro/TRMG)

## Répétitions
Cette leçon est répétitive et sera répétée chaque mois. Vous trouverez ci-dessous la liste des répétitions déjà organisées.

| Date        | Notes                                          |
|-------------|------------------------------------------------|
| 240102-2100 | First lesson                                   |
