---
layout: default
title: "Jade airgapped avec Sparrow Wallet"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Leçon Bitcoin-only</span> <span>Ce projet est maintenu par valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Jade airgapped avec Sparrow Wallet

![alt text](https://officinebitcoin.it/lezioni/jadespa/0.jpg)

Utiliser Jade pour des communications entièrement airgapped est possible grâce aux caractéristiques de son firmware et de son hardware.

La caméra intégrée et l'écran remplissent en effet exactement la fonction d'acquérir et d'envoyer des messages depuis et vers le wallet watch-only.

Ce tutoriel montre comment utiliser Jade airgapped avec Sparrow Wallet.

La procédure comprend d'abord la configuration, puis l'exportation de la clé publique étendue de Jade vers Sparrow-watch-only et, enfin, une transaction de dépense.

Par choix pédagogique, il a été décidé de commencer en montrant la séquence des opérations à partir de Jade.

## Configuration avancée

Le choix d'utiliser l'appareil en airgapped implique une vraie configuration, c'est-à-dire qu'elle doit être effectuée au moment de l'initialisation de Jade (1), qui doit donc se présenter comme non initialisé.

![alt text](https://officinebitcoin.it/lezioni/jadespa/1.jpg)

Un avis apparaît pour consulter les instructions de configuration sur le site https://blockstream.com/jade/.

![alt text](https://officinebitcoin.it/lezioni/jadespa/2.jpg)

La configuration de Jade pour une utilisation airgapped ne peut être effectuée qu'en choisissant Advanced Setup.

![alt text](https://officinebitcoin.it/lezioni/jadespa/3.jpg)

Jade avertit que cette configuration comporte certaines fonctions techniques avancées. Il suffit de faire très attention et de cliquer sur le bouton de confirmation.

![alt text](https://officinebitcoin.it/lezioni/jadespa/4.jpg)

Afin de saisir la mnémonique générée avec l'entropie des dés, choisis Restore Wallet.

![alt text](https://officinebitcoin.it/lezioni/jadespa/5.jpg)

Tu dois maintenant définir la longueur de la mnémonique, 12 ou 24 mots. Le menu offre aussi la possibilité de restaurer le wallet en scannant un code QR: il s'agit du SeedQr, qui a été traité dans le tutoriel dédié à la configuration.

![alt text](https://officinebitcoin.it/lezioni/jadespa/6.jpg)

Pour des raisons purement pédagogiques et de rapidité, ce tutoriel montre une configuration avec une mnémonique de 12 mots.

L'étape suivante doit être suivie comme décrit afin de pouvoir accéder à la fonctionnalité airgapped. Il faut en effet choisir d'exporter la phrase de récupération au format CompactSeedQR, en sélectionnant Yes.

![alt text](https://officinebitcoin.it/lezioni/jadespa/7.jpg)

Après ce choix, tu es averti qu'il faut dessiner le code QR sur le modèle fourni dans la boîte, comme indiqué dans la section "Extra" de la leçon dédiée à la configuration.

![alt text](https://officinebitcoin.it/lezioni/jadespa/8.jpg)

À la fin de la procédure, il faut vérifier la correspondance entre ce qui a été dessiné et le CompactSeedQR affiché par l'appareil. La caméra intégrée de Jade est en effet activée, et tu dois cadrer le SeedQR qui vient d'être dessiné.

![alt text](https://officinebitcoin.it/lezioni/jadespa/9.jpg)

Si le dessin correspond à ce que l'appareil a proposé dans la procédure qui vient d'être terminée, un signal de confirmation s'affiche.

![alt text](https://officinebitcoin.it/lezioni/jadespa/10.jpg)

Jade affiche maintenant les options de connexion de l'appareil à une companion app: choisis QR.

![alt text](https://officinebitcoin.it/lezioni/jadespa/11.jpg)

L'étape suivante demande également un choix à l'utilisateur: enregistrer les clés chiffrées sur l'appareil ou les charger à chaque session en scannant le SeedQR qui vient d'être dessiné.

![alt text](https://officinebitcoin.it/lezioni/jadespa/12.jpg)

Remarque:

Il est utile de comprendre ces deux options d'accès:

- QR PIN Unlock: Pendant l'initialisation, Jade enregistrera les données du wallet en les chiffrant sur l'appareil; elles seront toujours accessibles en déverrouillant Jade avec la procédure QR PIN.
- SeedQR: le SeedQR doit être scanné par Jade chaque fois que l'on veut charger les clés sur l'appareil.

Par choix pédagogique, l'option SeedQR a été choisie précédemment; l'appareil sera donc utilisé stateless: Jade avertit que la session est temporaire et que les clés seront "oubliées" par l'appareil lorsqu'il sera éteint.

![alt text](https://officinebitcoin.it/lezioni/jadespa/13.jpg)

Exportation de la clé publique

Maintenant que Jade est configuré spécifiquement pour fonctionner entièrement en airgapped, nous passons à la phase délicate de l'exportation de la clé publique.
 
En partant toujours de Jade, qui est revenu aux menus initiaux, choisis Options.

![alt text](https://officinebitcoin.it/lezioni/jadespa/14.jpg)

Remarque: le fait que Jade soit en mode Temporary Signer est visible grâce à l'icône représentant une horloge à côté de l'indication Active.

Dans Options, choisis Wallet

![alt text](https://officinebitcoin.it/lezioni/jadespa/15.jpg)

Sélectionne ensuite Export Xpub

![alt text](https://officinebitcoin.it/lezioni/jadespa/16.jpg)

À ce stade, l'écran de Jade affiche un code QR dynamique qui représente la clé publique étendue. Dans Options de ce sous-menu, tu peux choisir l'exportation multisig/singlesig et le chemin de dérivation.

Pour ce tutoriel, il a été choisi d'exporter un singlesig full segwit.

![alt text](https://officinebitcoin.it/lezioni/jadespa/17.jpg)

C'est à cette étape que Sparrow entre en jeu. Lance le programme et crée un nouveau wallet en choisissant New Wallet

![alt text](https://officinebitcoin.it/lezioni/jadespa/18.jpg)

Donne un nom au wallet, puis clique sur Create Wallet

![alt text](https://officinebitcoin.it/lezioni/jadespa/19.jpg)

Dans l'écran de paramètres suivant, clique sur Airgapped Hardware Wallet

![alt text](https://officinebitcoin.it/lezioni/jadespa/20.jpg)

Une fenêtre Sparrow s'ouvre et affiche les hardware wallets pris en charge. Choisis Jade

![alt text](https://officinebitcoin.it/lezioni/jadespa/21.jpg)

À ce stade, la caméra du PC avec lequel tu travailles est activée.

![alt text](https://officinebitcoin.it/lezioni/jadespa/22.jpg)

Si tu as plus d'une webcam disponible, sélectionne la meilleure dans le menu déroulant où apparaît Default Camera.

Prends maintenant Jade (qui continue entre-temps à afficher le code QR dynamique représentant le Xpub) et place l'écran devant la caméra du PC, en gardant le code QR à l'intérieur de l'espace en pointillés.

![alt text](https://officinebitcoin.it/lezioni/jadespa/23.jpg)

Sous l'image de la caméra, une barre de progression devient bleue.

La progression de l'acquisition du Xpub dans Sparrow est indiquée ainsi: de 0 à 100%.

À ce stade, quelques ajustements peuvent être nécessaires: augmenter/diminuer la luminosité de l'écran de Jade, ainsi que son éclairage frontal, ou choisir dans le menu déroulant de Sparrow Use HD Capture ou une réduction de résolution.

Ne sois pas impressionné par ces détails: une fois ton environnement de travail personnel réglé, ces phases se dérouleront avec confort et facilité. (2)

En effet, l'exportation a eu lieu lorsque la fenêtre de la caméra se ferme et, de retour dans les Settings de Sparrow, toutes les données du wallet watch-only apparaissent.

![alt text](https://officinebitcoin.it/lezioni/jadespa/24.jpg)

En raison de la structure de Sparrow, il faut maintenant appliquer la script policy en cliquant sur Apply.

La création du wallet se poursuit par la saisie et la confirmation d'un mot de passe pour chiffrer le fichier du wallet.

![alt text](https://officinebitcoin.it/lezioni/jadespa/25.jpg)

Elle se termine lorsque la barre de progression en bas à droite a rempli le champ à 100%.

![alt text](https://officinebitcoin.it/lezioni/jadespa/26.jpg)

## Transaction de dépense

Si, hypothétiquement, Jade joue le rôle de hardware wallet personnel, il faut supposer qu'il contient des fonds et que ceux-ci devront être dépensés à l'avenir.

Après avoir choisi Sparrow comme wallet watch-only et Jade comme dispositif de signature, voyons comment construire, signer et propager une transaction avec ces deux outils.

![alt text](https://officinebitcoin.it/lezioni/jadespa/27.jpg)

Dans l'exemple, un solde total de 56,598 sats est disponible.

Dans le menu de gauche de Sparrow, sélectionne Send et commence à construire la transaction de dépense. Après avoir tout réglé, clique sur Create transaction en bas à droite.

![alt text](https://officinebitcoin.it/lezioni/jadespa/28.jpg)

Une fenêtre avancée de transaction apparaît, où l'on voit que Sparrow reconnaît Jade comme dispositif de signature (Signing Wallet).

Si les paramètres conviennent, clique sur Finalize Transaction.

![alt text](https://officinebitcoin.it/lezioni/jadespa/29.jpg)

L'écran des signatures apparaît. Dans un système airgapped, l'exportation du .psbt se fait par code QR; dans Sparrow, clique donc sur Show QR en bas à gauche.

![alt text](https://officinebitcoin.it/lezioni/jadespa/30.jpg)

Une fenêtre apparaît avec un code QR dynamique représentant la psbt, qui devra ensuite être scannée avec la caméra de Jade.

![alt text](https://officinebitcoin.it/lezioni/jadespa/31.jpg)

Prends Jade et, depuis les menus principaux, sélectionne Scan QR

![alt text](https://officinebitcoin.it/lezioni/jadespa/32.jpg)

Cadre le code QR dynamique généré par Sparrow avec la caméra de Jade maintenant activée. Une barre bleue sur l'écran du hardware wallet indique le pourcentage d'avancement de la lecture.

Une fois l'importation de la psbt terminée, Jade affiche les détails de la transaction pour vérification: adresse de destination et montant sur un premier écran

![alt text](https://officinebitcoin.it/lezioni/jadespa/33.jpg)

puis les frais sur un second écran. En confirmant sur ce dernier, la signature est appliquée avec Jade.

![alt text](https://officinebitcoin.it/lezioni/jadespa/34.jpg)

Automatiquement, l'écran de Jade affiche un autre code QR dynamique: c'est la transaction signée.

Parmi les options de cet écran, tu peux augmenter/diminuer la densité pour améliorer la communication avec la wallet app.

![alt text](https://officinebitcoin.it/lezioni/jadespa/35.jpg)

Pendant ce temps, Sparrow, que nous avions laissé afficher un code QR dynamique, doit être réglé pour recevoir la transaction signée à propager.

Il faut donc cliquer sur Scan QR pour réactiver la webcam du PC.

![alt text](https://officinebitcoin.it/lezioni/jadespa/36.jpg)

Place l'écran de Jade devant la webcam et laisse Sparrow importer la transaction signée.

![alt text](https://officinebitcoin.it/lezioni/jadespa/37.jpg)

La barre de progression sous l'image doit atteindre 100% jusqu'à ce que l'importation se produise, ce que Sparrow affiche comme suit.

![alt text](https://officinebitcoin.it/lezioni/jadespa/38.jpg)

Toute la transaction est maintenant vérifiée à nouveau et, si elle est correcte, tu peux la propager en cliquant sur Broadcast Transaction.

Dans le menu Transactions, la transaction sortante apparaît.

![alt text](https://officinebitcoin.it/lezioni/jadespa/39.png)

Notes

- (1) – Si Jade est déjà initialisé, il suffit d'aller dans le menu Options → Settings → Factory reset
- (2) – Jade Original possède un très petit écran et, pour cadrer le code QR dynamique dans l'espace en pointillés affiché par Sparrow, il faut rapprocher l'écran à quelques centimètres. Il peut donc être nécessaire de se munir d'une webcam à très haute résolution avec une focale adaptée, ou de s'appuyer sur des apps comme Iriun pour "transformer" un téléphone en caméra du PC. Les téléphones ont en effet une meilleure capacité de mise au point à courte distance.
