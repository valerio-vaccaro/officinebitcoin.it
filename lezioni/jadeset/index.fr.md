---
layout: default
title: "Configuration de Jade"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Leçon Bitcoin-only</span> <span>Ce projet est maintenu par valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Configuration de Jade

![alt text](https://officinebitcoin.it/lezioni/jadeset/0_Cover.jpg)

Jade arrive dans un emballage dont l'intégrité doit être vérifiée, en contrôlant les deux autocollants holographiques anti-effraction placés entre la boîte (partie inférieure) et le couvercle (partie supérieure).

Le colis contient un petit manuel utilisateur, deux modèles CompactSeedQR, ainsi que le hardware wallet.

Jade s'allume en maintenant le bouton inférieur enfoncé et se présente avec les 3 menus:

- Setup Jade
- Scan QR
- Options

Dans Options, il est possible de régler différents paramètres selon les préférences personnelles, mais l'initialisation est la première partie à terminer.

Avec le bouton de défilement, sélectionne ensuite le menu __Setup Jade__ et confirme avec le bouton frontal.

![alt text](https://officinebitcoin.it/lezioni/jadeset/1.jpg)

Un avis apparaît pour consulter les instructions de configuration sur le site https://blockstream.com/jade/

![alt text](https://officinebitcoin.it/lezioni/jadeset/2.jpg)

Pour une exécution correcte, il est recommandé de créer la mnémonique avec des lancers de dés et d'utiliser cette entropie pour créer le wallet. Choisis donc __Advanced Setup__.

![alt text](https://officinebitcoin.it/lezioni/jadeset/3.jpg)

Jade avertit que cette configuration comporte certaines fonctions techniques avancées. Il suffit de faire très attention et de cliquer sur le bouton de confirmation.

![alt text](https://officinebitcoin.it/lezioni/jadeset/4.jpg)

Afin de saisir la mnémonique générée avec l'entropie des dés, choisis __Restore Wallet__.

![alt text](https://officinebitcoin.it/lezioni/jadeset/5.jpg)

Tu dois maintenant définir la longueur de la mnémonique, 12 ou 24 mots. Le menu offre aussi la possibilité de restaurer le wallet en scannant un code QR: il s'agit du SeedQr, qui sera abordé ailleurs.

![alt text](https://officinebitcoin.it/lezioni/jadeset/6.jpg)

Pour des raisons purement pédagogiques et de rapidité, ce tutoriel montre une configuration avec une mnémonique de 12 mots.

La procédure de saisie du premier mot commence et Jade affiche le clavier pour saisir les lettres correspondantes. Avec le bouton de défilement, place-toi ← → à la bonne position.

Dans cet exemple, le mot n° 1 est "below".

![alt text](https://officinebitcoin.it/lezioni/jadeset/7.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/8.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/9.jpg)

Après avoir saisi les 3-4 premières lettres, Jade sélectionne des mots dans le dictionnaire BIP39 et commence à proposer une série de suggestions. Avec le bouton de défilement, avance ou recule jusqu'à trouver le mot correct.

![alt text](https://officinebitcoin.it/lezioni/jadeset/10.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/11.jpg)

Continue la saisie des mots jusqu'au moment du dernier mot: le checksum.

À ce stade, Jade montre deux possibilités: saisir un mot existant ou offrir la possibilité de calculer un checksum valide avec son propre logiciel.

![alt text](https://officinebitcoin.it/lezioni/jadeset/12.jpg)

Remarque:

- Dans le cas d'une configuration à partir d'une mnémonique de 12 mots créée avec des lancers de dés, il est recommandé de choisir Existing et de saisir les premières lettres du mot, en les choisissant dans l'intervalle proposé par le lancer de dés.
- Si la configuration part plutôt d'une mnémonique de 24 mots générée avec des lancers de dés, tu peux demander à Jade de calculer tous les checksums possibles puis en choisir un. Il est vrai que l'on perd un peu d'entropie, mais seulement dans le dernier mot. Lorsque tu as décidé de confier tes fonds à Jade, c'est un compromis acceptable.
- En cas de restauration d'un wallet existant: saisis le checksum correct en choisissant Existing.

En poursuivant l'exemple de configuration à partir d'une mnémonique générée avec des lancers de dés, nous choisissons Existing dans le menu précédent, avec l'intention de saisir les lettres et de trouver le checksum correspondant.

![alt text](https://officinebitcoin.it/lezioni/jadeset/13.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/14.jpg)

À ce stade, Jade propose d'exporter la phrase de récupération sous forme de _CompactSeedQR_.

Le _CompactSeedQR_ est un encodage qui transforme la phrase mnémonique en un code QR à scanner pour restaurer le wallet sur Jade.

Si tu veux essayer, consulte la section au bas de ce tutoriel qui explique comment procéder.

![alt text](https://officinebitcoin.it/lezioni/jadeset/15.jpg)

En choisissant "No" dans le menu précédent, tu peux continuer jusqu'à la fin de la configuration.

L'appareil est prêt à être connecté à son wallet watch-only.

Le menu suivant montre les possibilités de connexion:

- USB
- QR code
- Bluetooth

![alt text](https://officinebitcoin.it/lezioni/jadeset/16.jpg)

Choisis USB et confirme avec le bouton de confirmation.

À ce stade, Jade demande à être connecté à une companion app.

Dans l'exemple suivant, il a été choisi de connecter l'appareil via USB à Blockstream Green; ce wallet permet en effet de contrôler les mises à jour du firmware de Jade et, en écoutant l'appareil via USB, offre une configuration guidée.

Ouvre Green et vérifie les paramètres réseau et de sécurité.

S'il existe une mise à jour du firmware, Green la signale immédiatement et il est recommandé d'effectuer la mise à niveau.

![alt text](https://officinebitcoin.it/lezioni/jadeset/17.jpg)

Une fois la mise à jour du firmware terminée, Green commence à interagir avec Jade.

Le dispositif de signature demande alors de définir le duress PIN, qui chiffrera les clés privées sur Jade, les rendant inaccessibles à toute personne sauf à celle qui possède le PIN à six chiffres.

![alt text](https://officinebitcoin.it/lezioni/jadeset/18.jpg)

Pendant que Green attend avec l'écran affiché ci-dessus, Jade propose de définir le PIN à 6 chiffres et de le confirmer en le saisissant à nouveau correctement.

![alt text](https://officinebitcoin.it/lezioni/jadeset/19.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/20.jpg)

Jade crée des données persistantes en les chiffrant sur l'appareil.

![alt text](https://officinebitcoin.it/lezioni/jadeset/21.jpg)

À la fin de l'opération, qui peut prendre quelques instants, Green ouvre le wallet prêt à l'emploi.

En éteignant Jade puis en le rallumant, l'appareil se présentera comme initialisé, avec un firmware à jour et prêt à être déverrouillé (Unlock Jade) pour être utilisé avec sa companion app.

![alt text](https://officinebitcoin.it/lezioni/jadeset/22.jpg)

## Extra: création du CompactSeedQR

À la fin de la saisie de la mnémonique, nous avons sauté la partie d'exportation des clés au format code QR afin de rester concentrés sur la phase de configuration. Ce type d'exportation peut toujours être effectué plus tard.

Allume Jade et, depuis le menu Options → Temporary Signer → Continue → 12/24 Words, tu reviens au menu de saisie de la phrase de récupération, à la fin duquel l'écran de choix pour l'exportation au format SeedQR est proposé.

![alt text](https://officinebitcoin.it/lezioni/jadeset/15.jpg)

En choisissant Yes, tu es averti qu'il faut dessiner le code QR sur le modèle fourni dans la boîte.

![alt text](https://officinebitcoin.it/lezioni/jadeset/24.jpg)

La procédure commence par afficher une vue d'ensemble de ce que sera le code QR à dessiner (certaines parties sont effacées pour des raisons de confidentialité).

![alt text](https://officinebitcoin.it/lezioni/jadeset/25.jpg)

Ensuite, toutes les cases de la grille seront affichées, une par une, de A1 à C3 ou E5 selon la longueur de la phrase de récupération.

![alt text](https://officinebitcoin.it/lezioni/jadeset/26.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/27.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/28.jpg)

Après avoir dessiné la dernière case de la grille, Jade affiche de nouveau la vue d'ensemble pour une première vérification. Continue en confirmant Done.

![alt text](https://officinebitcoin.it/lezioni/jadeset/29.jpg)

La caméra intégrée de Jade est activée; avec elle, tu dois cadrer le SeedQR qui vient d'être dessiné.

![alt text](https://officinebitcoin.it/lezioni/jadeset/30.jpg)

Si le dessin correspond à ce que Jade a proposé dans la procédure qui vient d'être terminée, un signal de confirmation s'affichera.

![alt text](https://officinebitcoin.it/lezioni/jadeset/31.jpg)

En cliquant pour confirmer Continue, Jade se présente en fonctionnement depuis les menus principaux.

Le CompactSeedQR est un outil permettant de restaurer le wallet sur Jade.
