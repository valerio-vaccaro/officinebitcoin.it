---
layout: default
title: "Installation de Debian"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Leçon Bitcoin-only</span> <span>Ce projet est maintenu par valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Installation de Debian
Nous préparons une clé USB avec l'image Debian téléchargée depuis le site officiel.

Nous branchons tous les câbles (display, keyboard, mouse, and ethernet).

![alt text](https://officinebitcoin.it/lezioni/debian/1.jpg)

Nous branchons la clé USB d'installation.

![alt text](https://officinebitcoin.it/lezioni/debian/2.jpg)

Nous allumons l'ordinateur et nous assurons que notre clé USB avec Debian démarre.

![alt text](https://officinebitcoin.it/lezioni/debian/3.jpg)

## Installation
Si tout a fonctionné correctement, l'installateur Debian devrait démarrer et nous arriverons à l'écran suivant.

![alt text](https://officinebitcoin.it/lezioni/debian/4.jpg)

Nous choisissons la première ligne et lançons l'installation graphique.

La première chose qui nous sera demandée est la langue ; pour cette installation, je choisirai "English", que je trouve plus compréhensible que toute autre traduction.

![alt text](https://officinebitcoin.it/lezioni/debian/5.jpg)

À ce stade, notre emplacement géographique nous sera demandé ; pour trouver l'Italie, nous devons sélectionner OTHER->EUROPE->ITALY.

![alt text](https://officinebitcoin.it/lezioni/debian/6.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/7.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/8.jpg)

Pour la localisation, je choisis également English ici.

![alt text](https://officinebitcoin.it/lezioni/debian/9.jpg)

Et je configure le clavier italien, puisque c'est celui dont je dispose.

![alt text](https://officinebitcoin.it/lezioni/debian/10.jpg)

Nous choisissons ensuite un nom d'utilisateur et laissons le domaine vide.

![alt text](https://officinebitcoin.it/lezioni/debian/11.jpg)

À ce stade, Debian vous demandera de choisir un mot de passe pour l'utilisateur root...

![alt text](https://officinebitcoin.it/lezioni/debian/12.jpg)

et de créer un utilisateur avec son mot de passe respectif.

![alt text](https://officinebitcoin.it/lezioni/debian/13.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/14.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/15.jpg)

Nous devons maintenant choisir le disque d'installation ; nous utiliserons tout le disque et devons sélectionner le disque sur lequel effectuer l'installation.

![alt text](https://officinebitcoin.it/lezioni/debian/16.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/17.jpg)

Nous devons ensuite sélectionner la structure des partitions ; pour l'instant, nous laisserons tout dans une seule partition.

![alt text](https://officinebitcoin.it/lezioni/debian/18.jpg)

Debian propose une table de partitions, mais... il a ajouté du swap, ce que nous ne voulons pas, alors sélectionnons-le et supprimons-le de la liste.

![alt text](https://officinebitcoin.it/lezioni/debian/19.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/20.jpg)

Maintenant que nous l'avons supprimé, nous pouvons enfin écrire notre table.

![alt text](https://officinebitcoin.it/lezioni/debian/21.jpg)

Debian voudrait revenir à la configuration de la table de partitions, mais nous déclinons l'invitation.

![alt text](https://officinebitcoin.it/lezioni/debian/22.jpg)

Et nous confirmons l'intention d'écrire la table mise à jour.

![alt text](https://officinebitcoin.it/lezioni/debian/23.jpg)

On nous demande maintenant si nous voulons utiliser un mirror Debian ; nous choisissons de l'utiliser.

![alt text](https://officinebitcoin.it/lezioni/debian/24.jpg)

Nous choisissons notre pays.

![alt text](https://officinebitcoin.it/lezioni/debian/25.jpg)

Habituellement, le mirror GARR est rapide et fiable ; utilisons celui-là.

![alt text](https://officinebitcoin.it/lezioni/debian/26.jpg)

Je n'ai aucun proxy, donc je laisse le champ vide.

![alt text](https://officinebitcoin.it/lezioni/debian/27.jpg)

Mais quels programmes installer ? Comme nous préparons un serveur, nous désactivons l'environnement graphique (en retirant les deux premières coches) et sélectionnons SSH, dont nous aurons besoin pour l'accès à distance.

![alt text](https://officinebitcoin.it/lezioni/debian/28.jpg)

L'installation commence.

À la fin, on nous demande si nous voulons installer grub, qui nous permet de démarrer Linux ; nous répondons par l'affirmative et choisissons le même disque que celui sur lequel nous avons installé le système d'exploitation.

![alt text](https://officinebitcoin.it/lezioni/debian/29.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/30.jpg)

Yuhuuu, c'est terminé ; il est temps de retirer la clé USB et de redémarrer la machine.

![alt text](https://officinebitcoin.it/lezioni/debian/31.jpg)

Si tout a fonctionné correctement, nous devrions nous retrouver devant un terminal qui nous demande de nous connecter avec l'un des profils créés pendant l'installation.

## Configuration

### Connectons-nous
Nous nous connectons à notre serveur avec `ssh username@ip`, où username sera le nom choisi pendant l'installation et ip l'adresse IP de l'ordinateur sur lequel nous avons installé.

Évidemment, cette étape peut être ignorée si vous installez avec un écran et un clavier au lieu de vous connecter par le réseau.

Notez que Debian INTERDIT de se connecter via ssh en utilisant les identifiants du superutilisateur (c'est-à-dire root).

### Dépôt
Maintenant, mettons à jour les dépôts.

Nous devenons superutilisateur avec la commande `su` et en saisissant le mot de passe root.

Nous modifions le fichier des dépôts avec la commande `nano /etc/apt/sources.list` et supprimons toutes les lignes présentes.

Nous ajoutons les lignes suivantes.

```                                                                    
deb http://deb.debian.org/debian/ bookworm contrib main non-free non-free-firmware
# deb-src http://deb.debian.org/debian/ bookworm contrib main non-free non-free-firmware

deb http://deb.debian.org/debian/ bookworm-updates contrib main non-free non-free-firmware
# deb-src http://deb.debian.org/debian/ bookworm-updates contrib main non-free non-free-firmware

deb http://deb.debian.org/debian/ bookworm-proposed-updates contrib main non-free non-free-firmware
# deb-src http://deb.debian.org/debian/ bookworm-proposed-updates contrib main non-free non-free-firmware

deb http://deb.debian.org/debian/ bookworm-backports contrib main non-free non-free-firmware
# deb-src http://deb.debian.org/debian/ bookworm-backports contrib main non-free non-free-firmware

deb http://deb.debian.org/debian-security/ bookworm-security contrib main non-free non-free-firmware
# deb-src http://deb.debian.org/debian-security/ bookworm-security contrib main non-free non-free-firmware

```

Nous pouvons ensuite enregistrer le fichier en appuyant sur `CTRL+x` puis sur `y`.

La commande `apt update` nous permet de vérifier que tout s'est bien passé et de mettre à jour la liste des paquets.

### Mettre à jour le système
Pour mettre à jour le système, il suffit d'exécuter les commandes suivantes :

- `apt update` pour mettre à jour la liste des paquets,
- `apt upgrade` pour mettre à jour les paquets installés pour lesquels une nouvelle version existe.

### Installer tor et l'utiliser avec ssh
Pour installer tor, il suffit d'utiliser la commande `apt install tor`.

Une fois installé, nous pouvons le configurer avec la commande suivante `nano /etc/tor/torrc`.

À la fin du fichier, nous ajoutons les lignes suivantes.

```
HiddenServiceDir /var/lib/tor/hidden_service/
HiddenServicePort 22 127.0.0.1:22
```

Et nous redémarrons tor avec `systemctl restart tor` ; nous pouvons maintenant trouver notre adresse onion avec `cat /var/lib/tor/hidden_service/hostname`.

En utilisant tor, nous pouvons maintenant nous connecter à notre machine depuis n'importe où dans le monde avec `torify ssh username@onionaddress.onion`.

## Programme
L'installation de Debian est une leçon répétitive ; voici une liste de celles déjà organisées :

| Date        | Notes                                          |
|-------------|------------------------------------------------|
| 240415-2200 | Première leçon                                 |
