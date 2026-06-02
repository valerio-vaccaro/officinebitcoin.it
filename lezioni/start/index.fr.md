---
layout: default
name: "Kit de démarrage Bitcoin"
description: "Un kit de démarrage simple et facile à mettre en place pour utiliser Bitcoin correctement. Apprenez à télécharger et installer une wallet mobile, configurer un POS pour les demandes de paiement et découvrir les réglages avancés de la wallet."
title: "Glossaire initial"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Leçon Bitcoin-only</span> <span>Ce projet est maintenu par valerio-vaccaro</span></p>

## 🌍 Traductions

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

![cover](assets/cover.webp)

Voici une excellente façon de commencer à utiliser Bitcoin de la manière la plus correcte possible. Ce qui suit est une proposition de *starter kit* très léger et facile à mettre en place, que vous pouvez configurer en autonomie.

Que vous soyez un utilisateur curieux, un professionnel qui veut accepter Bitcoin comme moyen de paiement, ou un utilisateur expérimenté à la recherche de solutions pour ses proches, ce guide vous permettra de :
- télécharger et installer une wallet mobile pour utiliser Bitcoin à tous les niveaux (onchain pour la conservation longue durée ; ou Liquid et Lightning pour les paiements instantanés) ;
- configurer un POS pour générer des demandes de paiement à partir du prix de vos biens/services en euros ;
- découvrir les réglages avancés de la wallet. Nous avons laissé cette partie à la fin du guide pour simplifier la première approche, mais consultez-la toujours, car elle est importante.

Clarifions d'abord ce que nous voulons dire lorsque nous parlons d'utiliser Bitcoin de la façon *correcte*.

# Glossaire initial
- `Not your keys, not your coins`
  Si vous découvrez Bitcoin, l'expression `Not your keys, not your coins` est nouvelle pour vous et son sens se limite peut-être à sa traduction littérale. Bitcoin fonctionne sur le principe de la cryptographie asymétrique, fondée sur des paires de clés publiques et privées. C'est avec la possession **unique** et la gestion individuelle des clés privées que vous pouvez dire que vous contrôlez vos Bitcoin.
  
  Vous devez donc être la seule personne à connaître les clés privées, le secret qui vous permettra de posséder et, éventuellement, de dépenser les bitcoin associés à ces clés. `Not your keys, not your coins` est pratiquement un _mantra_ pour les bitcoiners du monde entier, et il le deviendra aussi pour vous.

- `Recovery phrase`
  Au cours de sa brève histoire, le protocole Bitcoin a évolué pour rendre plus simple la gestion des secrets, c'est-à-dire des clés privées. Aujourd'hui, elles sont représentées sous la forme d'une suite de 12 ou 24 mots anglais, plus facile à transcrire et à vérifier. Ces mots sont le secret principal à conserver. Ils doivent être recopiés sur papier et gardés dans un lieu très sûr, par exemple un coffre. Ils ne doivent jamais être photographiés, transférés sur un ordinateur ni, encore moins, partagés avec d'autres personnes.

- `Wallet`
  La wallet est l'outil qui vous permettra de voir votre solde, d'accepter des Bitcoin et d'en dépenser. Dans ce tutoriel, nous en téléchargerons une sur votre téléphone. La wallet sur téléphone s'appelle `hot wallet`, car elle est hébergée sur un appareil toujours connecté à internet. Si vous débutez, c'est parfaitement adapté ; avec l'étude, vous apprendrez d'autres méthodes pour perfectionner l'utilisation de votre wallet.

- `Non Custodial`
  Il est fondamental de commencer à utiliser Bitcoin avec des wallets `non-custodial`, c'est-à-dire celles qui **vous donnent le contrôle complet des clés privées**. Méfiez-vous toujours de ceux qui vous poussent à utiliser d'autres outils, dits custodial, pour approcher Bitcoin. Les wallets custodial sont des outils dont vous ne possédez pas les clés. Ce n'est pas une question de **si**, mais de **quand** ils vous empêcheront définitivement d'accéder à vos fonds.

# Blockstream App (ex Green Wallet)
Pour le starter kit, nous allons télécharger Blockstream App, une wallet `open source` dont vous pouvez vérifier le code. L'application a une longue tradition de développement et un historique solide ; la wallet s'est montrée fiable par le passé.

---
⚠️ Les instructions suivantes concernent le téléchargement et l'installation de l'app pour Android. Pour iOS, vous devez utiliser la boutique officielle.

---

## 🌍 Traductions

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

Rendez-vous sur https://github.com/Blockstream/green_android, le dépôt Github officiel du développeur.

![img](assets/01.webp)

Au milieu de la page, à droite, sélectionnez `Latest` dans l'espace consacré aux *Releases* afin de télécharger la version la plus récente.

Vous arriverez sur une page affichant la dernière release, 5.1.4 au moment de la rédaction de ce tutoriel en décembre 2025. Sur cette même page, sélectionnez ce que vous pouvez télécharger :

![img](assets/02.webp)

Téléchargez le fichier `.apk` sans passer par le Play Store et installez-le sur votre téléphone Android.

![img](assets/03.webp)

---
⚠️ Votre téléphone peut demander des autorisations spéciales pour télécharger des apps depuis des sources non certifiées. Accordez ces autorisations pour continuer.

---
Lorsque Android vous demande d'installer Blockstream App, cliquez sur `Install`.

![img](assets/04.webp)

À la fin de l'installation, choisissez `Open`.

![img](assets/05.webp)

Blockstream App s'ouvre et, pour commencer à utiliser la wallet, choisissez `Get Started`.

![img](assets/07.webp)

Blockstream vous demandera si vous souhaitez participer à la collecte de données pour aider les développeurs à améliorer l'app. Refusez l'invitation.

![img](assets/08.webp)

# Votre première wallet
Vous pouvez commencer à créer votre première wallet. Cliquez sur `Set Up Mobile Wallet`.

![img](assets/09.webp)

Le processus de création de la wallet commence.

![img](assets/10.webp)

Il se termine en quelques secondes. Votre wallet est prête et, pour commencer à l'utiliser, cliquez sur `Continue`.

![img](assets/11.webp)

La wallet s'ouvre sur l'écran appelé `Home`. Pour l'instant, observez-le, mais concentrez-vous tout de suite sur le menu inférieur `Security`.

# Vos clés, vos coins

![img](assets/12.webp)

Dans ce menu, il vous sera demandé de sauvegarder votre wallet. Cela consiste simplement à afficher la suite de 12 mots dont vous aurez besoin pour la restaurer à l'avenir. Ces 12 mots sont votre wallet : **assurez-vous d'être dans un environnement sûr, à l'abri des regards indiscrets, et d'avoir un carnet ou une feuille pour transcrire les mots avant de les placer dans un lieu sûr** (par exemple un coffre). Cliquez sur `Back Up Now` et découvrez les 12 mots.

**Notez aussi l'ordre exact des mots : 1, 2, 3, etc. ; écrivez les mots en majuscules pour mieux les relire plus tard, mais souvenez-vous que si vous devez les saisir manuellement à l'avenir, vous devrez utiliser les minuscules**.

![img](assets/13.webp)

Après avoir transcrit et placé les mots en lieu sûr, poursuivez le starter kit. Tous les autres réglages se trouvent à la fin du guide.

# Menu TRANSACT
Utiliser la wallet est extrêmement simple :
- allez dans le menu `Transact`
- il existe deux commandes principales : `Send` et `Receive` (**ignorez `Buy`**).

![img](assets/17.webp)

Lorsque vous aurez des transactions, elles seront visibles sous les commandes. Comme vous n'avez pas encore de fonds, sélectionnez `Receive` pour commencer à en recevoir.

Une série d'*Assets* apparaît, mais concentrez-vous uniquement sur Bitcoin. Vous pouvez choisir entre Bitcoin onchain (icône orange) et Liquid (icône bleue), qui vous permettra de profiter de paiements instantanés, comme avec Lightning Network, mais au moyen d'un mécanisme que nous verrons plus loin.

Pour commencer, choisissez Bitcoin Onchain, l'icône orange.

![img](assets/18.webp)

Ce qui apparaît est un code QR représentant l'une de vos adresses Bitcoin, que vous voyez aussi en bas avec le libellé `bc1q` suivi d'autres caractères. Vous pouvez montrer le code QR à une personne qui doit vous payer afin de recevoir vos premiers fonds, de petites fractions raisonnables de Bitcoin, aussi appelées `Satoshi`.

![img](assets/19.webp)

Si vous revenez en arrière et choisissez Liquid, le menu indique ⚡️**Lightning Ready**. Sachez qu'en utilisant un service de `SWAP`, Blockstream App vous permettra de recevoir des paiements presque instantanés, d'émettre des demandes de paiement Lightning Network ou de payer des factures LN, en déposant/retirant des fonds depuis un compte Liquid de cette même wallet.

![img](assets/20.webp)

Dans le menu qui s'ouvre après ce choix, sélectionnez comment vous voulez recevoir des fonds, entre Liquid et Lightning. Si vous choisissez Liquid, un code QR semblable à celui affiché avec Bitcoin Onchain apparaîtra ; il représente une adresse reconnaissable au préfixe `lq1q` suivi d'autres caractères.

Si vous sélectionnez Lightning, il vous sera demandé de saisir le montant à recevoir et de confirmer en cliquant sur `Confirm`.

![img](assets/21.webp)

Blockstream App vous montre un code QR représentant la facture LN, payable avec n'importe quelle wallet Lightning Network.

![img](assets/22.webp)

---
⚠️ Dans notre simulation, nous avons demandé à recevoir 210 sats, mais le code QR obtenu indique que nous recevrons 160 sats. Les swaps ont en effet un coût, environ 50 satoshis pour chaque paiement reçu. **Il est important de garder cet aspect à l'esprit, surtout lors de la réception de micropaiements**. Rien ne change pour le payeur, qui verra bien le montant demandé déduit de la demande créée lors de la configuration : 210 satoshis.

---

# Vous êtes commerçant ? Utilisez le POS
Pour faire de ce guide un véritable **starter kit**, nous pouvons associer les encaissements Bitcoin sur cette wallet à un POS externe.

Vous pouvez le configurer en quelques étapes directement sur https://btcpos.cash/.

![img](assets/23.webp)

Vous pourrez ainsi recevoir des paiements Lightning directement sur la wallet créée avec Blockstream App, partager le lien avec des collaborateurs et, pour cela, suivre simplement les prochaines étapes afin de créer un lien à garder à portée de main sur l'écran d'accueil de votre téléphone. Il vous faut copier le `Descriptor` de votre wallet et le coller dans le grand espace central du site.

# 1. Recevoir les premiers fonds sur le réseau Liquid
Il faut activer l'affichage des *Assets* sur l'écran d'accueil de votre wallet. Si elle vient d'être créée, vous devez encaisser une facture LN ou recevoir des fonds sur une adresse Liquid.

Après avoir reçu des fonds, vous pouvez sélectionner Liquid parmi les `Assets` visibles dans le menu `Home`.

![img](assets/24.webp)

# 2. Accéder aux paramètres nécessaires
Vous avez maintenant ce qu'il faut pour accéder aux paramètres qui permettront de « transporter » votre wallet vers le POS. Techniquement, cela s'appelle *exportation de clé publique* ; c'est un détail que vous apprendrez par l'étude approfondie. Pour l'instant, sachez qu'il suffit de sélectionner le menu en haut à droite :

![img](assets/25.webp)

Puis choisissez `Watch-only` dans le menu déroulant qui apparaît.
![img](assets/26.webp)

`Output Descriptors` apparaît : c'est exactement le paramètre recherché. Copiez-le avec la commande prévue et retournez sur la page web où vous configurez le POS.

![img](assets/27.webp)

# 3. Configurer le POS
Collez le descriptor dans l'espace prévu et cliquez sur `GENERATE POS LINK`. Le système créera une URL unique, valable seulement pour vous et votre wallet.

![img](assets/28.webp)

Vous pouvez aussi définir d'abord la devise de référence, en choisissant USD, CHF ou EUR dans le menu déroulant où apparaît `Currency`.
![img](assets/29.webp)

# 4. Encaisser en générant des demandes de paiement avec le POS
Une fois que vous avez cliqué sur `GENERATE POS LINK`, la page affiche le résultat : **le lien a été créé avec succès**. Vous pouvez le copier, car il restera toujours accessible **uniquement pour votre wallet** à l'URL générée.

![img](assets/30.webp)

Vous pouvez aussi ouvrir le POS et commencer à l'utiliser :
![img](assets/31.webp)

Supposons, par exemple, que vous vouliez générer une facture de 3 351 sats en y associant une description.

![img](assets/32.webp)

En cliquant sur `CREATE INVOICE`, le POS affiche le code QR ou la facture textuelle à présenter à un client potentiel.

![img](assets/33.webp)

Lorsque le client a payé la facture, sur laquelle il lira correctement la *description* (Coppa del Nonno dans cet exemple), le POS signale le paiement reçu.

![img](assets/34.webp)

Ce paiement est aussi correctement visible dans la wallet.
![img](assets/35.webp)

Il ne vous reste qu'à mémoriser et garder à portée de main le lien du POS, pour l'utiliser au besoin, même sur le téléphone où vous avez installé votre wallet.

![img](assets/36.webp)

Ajoutez-le comme lien/app sur l'écran d'accueil

![img](assets/37.webp)

# ⚠️ NOTE IMPORTANTE
Si vous relisez les étapes qui viennent d'être effectuées concernant l'encaissement de la facture dans ce dernier exemple, deux choses importantes apparaissent :
1. le client a vu une facture de 3 351 sats
2. notre wallet a encaissé 3 293 sats.

Avant de crier au scandale, il faut revenir à l'écran initial du POS, qui affiche le texte visible dans l'image ci-dessous :

![img](assets/38.webp)

La différence entre 3 351 (facture présentée au client) et 3 293 (votre encaissement) tient exactement à ceci :
- 50 sats pour chaque facture générée
- 0,25 % de frais de service (8 sats = 0,25 % de 3 351)
- Total encaissé : 3 293

#### Vous débutez et ceci est un starter kit. De petits frais sont le compromis pour utiliser Bitcoin en self-custody, sans intermédiaires, et profiter de toutes les possibilités, y compris les petits paiements instantanés.

#### Avec l'étude, vous apprendrez à utiliser d'autres outils qui ne demanderont pas d'autres frais que ceux également prévus pour les utilisateurs expérimentés.

---
# Autres réglages

Il est temps de bien connaître votre première wallet. Les réglages sont importants, car ils vous aideront dans l'utilisation quotidienne.

## Menu
Les menus de Blockstream App se trouvent en bas et sont :
- Home
- Transact
- Security
- Settings

Continuez à configurer votre wallet depuis le menu `Security`. En plus de la possibilité de voir et transcrire les mots de la `Recovery phrase`, ce menu met à votre disposition d'autres fonctions importantes.

Vous pouvez par exemple configurer la connexion à votre wallet avec le contrôle biométrique (s'il est activé sur votre téléphone) ou ajouter un PIN à six chiffres pour accéder à la wallet. Ces options sont très importantes, car elles empêchent des inconnus d'accéder à votre wallet et de la consulter s'ils ont votre téléphone en main.

![img](assets/14.webp)

Dans ce menu, vous pouvez aussi décider du délai de *Logout*, c'est-à-dire le moment où la wallet se déconnecte après quelques minutes d'inactivité. Par défaut, il est réglé sur *5 minutes* et vous pouvez le modifier selon vos besoins, plus long ou plus court, en fonction de votre aisance manuelle.
![img](assets/15.webp)
# Menu SETTINGS
Menu très important, car il contient tous les réglages de la wallet. En cliquant dans ce menu, vous pouvez par exemple renommer la wallet : dans notre exemple, nous l'avons appelée *Starter Kit*. Renommer les wallets pour les distinguer est très important lorsque vous en utilisez plusieurs sur le même appareil et devez comprendre/choisir laquelle utiliser.

![img](assets/39.webp)

Si vous allez plutôt dans le sous-menu `Denomination`, vous trouverez des réglages très utiles concernant la devise.
![img](assets/40.webp)

Je recommande d'utiliser `satoshi/sats` comme unité pour les montants en Bitcoin. Le Satoshi est la plus petite unité de BTC, égale à un cent millionième de Bitcoin. Le choix de l'exchange de référence pour la conversion apparaîtra également. Utilisez-en un qui permette d'afficher et de définir des montants en EUR.

![img](assets/41.webp)

Enfin, dans le menu `Settings`, vous pouvez vérifier la version actuellement utilisée de Blockstream App et voir si elle doit être mise à jour, ainsi que les commandes pour demander de l'aide directement *in-app*.
![img](assets/42.webp)

# Menu HOME
Le `Home` de Blockstream App est le menu dans lequel votre wallet s'ouvre à chaque nouvel accès. En faisant défiler vers le bas, vous trouverez l'option d'acheter Bitcoin via un exchange intégré. **Ne l'utilisez pas**.

![img](assets/16.webp)

# Restauration de la wallet
Si, pendant l'utilisation, vous vous rendez compte que vous devez changer de téléphone ou utiliser la wallet *Starter Kit* sur plusieurs appareils, sachez qu'avec Blockstream App vous pouvez le faire.

Pour continuer, il suffit d'apprendre la procédure de restauration de la wallet, expliquée ci-dessous, qui inclut les étapes à suivre si vous perdez l'accès au téléphone sur lequel vous avez commencé à utiliser la wallet.

Vos fonds ne sont en réalité ni « sur le téléphone » ni « dans la wallet ». Les fonds sont sur le réseau Bitcoin, qu'il s'agisse d'Onchain, de Lightning ou de Liquid. La wallet, plus précisément les clés publiques et privées de votre wallet, est l'outil permettant d'accéder aux adresses utilisées et, avec elles, au solde associé.

C'est pour cette procédure que vous avez transcrit les 12 mots et les avez placés en lieu sûr... **Vous l'avez fait, n'est-ce pas ?** Car sans ces mots, vous n'aurez plus accès à vos fonds.

# a. Nouvelle installation de Blockstream App
Installez d'abord de nouveau Blockstream App avec la procédure montrée au début. Une nouvelle release peut être arrivée entre-temps ; utilisez la plus récente.

Lancez Blockstream App sur le nouvel appareil et continuez en cliquant sur `Get Started` puis en refusant la collecte de données.

# b. Restaurer depuis une sauvegarde
Les ressemblances avec la première installation s'arrêtent ici. Lorsque l'écran de création de la wallet apparaît, au lieu de choisir `Set Up Mobile Wallet` comme la première fois, choisissez `Restore from backup`.

![img](assets/43.webp)

Si vous utilisez le réseau principal de Bitcoin, c'est-à-dire celui qui utilise de vrais fonds, choisissez `Mainnet` sur l'écran suivant.

![img](assets/43.webp)

L'écran avec les champs où saisir les mots de la `Recovery phrase` apparaît. Réécrivez-les dans l'ordre et correctement, puis sélectionnez `Continue` pour recréer la wallet sur le nouvel appareil.

![img](assets/45.webp)

La phase de restauration de la wallet peut prendre quelques minutes ; attendez patiemment qu'elle se termine correctement. À la fin du processus, vous retrouverez votre wallet, avec le solde et l'historique des transactions.

![img](assets/46.webp)

---
⚠️ La wallet recréée sur le nouvel appareil est active à 100 %. Cela signifie qu'elle possède aussi les clés privées permettant de dépenser. Gardez-le à l'esprit si vous voulez la confier à un collaborateur pour votre activité.

**Utilisez plutôt le lien POS pour les collaborateurs, car il a été créé uniquement avec la clé publique (le `descriptor`)**.

---

# Comment continuer à apprendre ?

![img](assets/47.webp)
![img](assets/48.webp)
