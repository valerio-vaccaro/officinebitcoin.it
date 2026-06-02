---
layout: default
title: "Lightning Network non-custodial"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Leçon Bitcoin-only</span> <span>Ce projet est maintenu par valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

![cover](https://officinebitcoin.it/lezioni/canale/01cover.webp)

# Lightning Network non-custodial
Phoenix d'Acinq est un wallet Lightning Network natif, non-custodial, qui offre un wallet efficace conforme au standard BIP39, bien connecté, tout en laissant le contrôle complet aux utilisateurs.

Vous découvrirez vite que Phoenix ouvre un canal LN, dont vous êtes responsable du solde à 100 %.
Pour bien travailler avec Phoenix, il suffit d'une attention minimale et de connaissances de base de la Lightning Network. Vous apprendrez par exemple à garder la liquidité de votre canal sous contrôle, à le maintenir équilibré selon vos besoins et à vous assurer qu'Acinq vous voit en ligne, afin de le garder ouvert et de maintenir l'infrastructure LN.

# Opérations de base
Après avoir [téléchargé et vérifié l'apk Phoenix](https://officinebitcoin.it/lezioni/verifica/index.html), vous pouvez installer l'app sur votre téléphone.

Phoenix s'ouvre en vous demandant si vous voulez créer un nouveau wallet ou restaurer un wallet précédent. Si c'est votre première expérience avec Phoenix, choisissez `Create new wallet`. Une série d'écrans d'accueil suivra, et se terminera là où vous appuierez sur `Get started`.

![img](https://officinebitcoin.it/lezioni/canale/03.webp)

## Backup
Une fois Phoenix ouvert, **la première opération à faire est, comme toujours, le backup du wallet**.

Phoenix adopte le standard BIP39, chemin de dérivation m/84'/0'/0', en fournissant une séquence de 12 mots à transcrire sur papier et à conserver dans un endroit sûr.

![img](https://officinebitcoin.it/lezioni/canale/04.webp)

Entrez dans les menus et demandez à Phoenix de vous afficher la *Recovery phrase*, en cliquant sur `Display seed`.

![img](https://officinebitcoin.it/lezioni/canale/05.webp)

Une fois terminé, pensez à faire défiler l'écran jusqu'en bas pour confirmer que vous avez effectué le backup et ne plus voir la notification ni l'alerte.

![img](https://officinebitcoin.it/lezioni/canale/06.webp)

Phoenix est essentiellement prêt à être utilisé. Votre nouveau wallet a un solde nul et peut être configuré. En bas à gauche, vous trouverez la commande pour revenir dans les paramètres et configurer des options utiles au quotidien.

![img](https://officinebitcoin.it/lezioni/canale/07.webp)

## Utilisation avec Tor
Depuis plusieurs versions de Phoenix, Acinq a désactivé le moteur Tor intégré. Si vous voulez utiliser Phoenix avec la protection de Tor, deux étapes sont nécessaires :
- activer Tor dans les paramètres de Phoenix
- utiliser une app tierce pour acheminer le trafic du wallet via le réseau onion.

Accédez aux paramètres et choisissez Tor, puis activez `Enable Tor`, et enfin acheminez le trafic via l'app que vous utilisez habituellement (Orbot, Invizible Pro, etc.). Sans l'une de ces apps tierces, mais avec Tor activé dans les paramètres de Phoenix, le wallet ne pourra pas se connecter à internet.

![img](https://officinebitcoin.it/lezioni/canale/09.webp)

## Autres paramètres
Vous pouvez modifier ou définir plusieurs fonctions :
- le nom du wallet, en cliquant sur le mot `Wallet` en haut ;
- la devise de référence depuis le sous-menu `Display`.
- définir les frais dans `Channel management`, un paramètre important car une valeur de frais trop basse pourrait compromettre l'ouverture du canal : par défaut elle est fixée à 5,000 sats, augmentez-la à 15,000 ; Phoenix utilisera de toute façon la valeur appropriée au moment voulu ;
- vous devriez configurer toutes les précautions de sécurité que vous pensez pouvoir gérer, dans le sous-menu `Access control` : PIN pour dépenser, PIN ou contrôle biométrique pour accéder à l'app ;
- configurer votre propre `Electrum server` dans le menu du même nom, en notant que Phoenix exige un certificat SSL valide (Let's Encrypt, par exemple) ;
- activer `Experimental features` pour demander une adresse LN Bolt12 réutilisable
- gérer d'éventuelles fermetures de canaux ou la création/suppression de plusieurs wallets.

![img](https://officinebitcoin.it/lezioni/canale/08.webp)

# Ouverture d'un canal LN ⚡️

Depuis l'écran principal de Phoenix, choisissez la commande `Receive`

![img](https://officinebitcoin.it/lezioni/canale/10.webp)

Le wallet vous propose deux modes de réception, tous deux avec QR code : Lightning et Onchain.

## Payer une facture Lightning

![img](https://officinebitcoin.it/lezioni/canale/11.webp)

Une façon rapide d'ouvrir votre canal LN consiste à créer une facture avec Phoenix et à la payer avec un autre wallet LN.

Le premier paiement entrant détermine l'ouverture d'un canal, dont la liquidité est définie par le montant de la facture que vous venez de créer (hors frais de la transaction onchain d'ouverture du canal).

Les fonds peuvent être disponibles immédiatement, malgré l'affichage d'un avis temporaire d'attente de confirmations onchain. Ou vous devrez peut-être attendre pour les utiliser.

## Transaction onchain
L'ouverture d'un canal LN est toujours une transaction onchain, multisig 2-de-2 : vous et la contrepartie (Acinq) établissez les conditions, avec vos fonds.

Si vous n'avez pas la possibilité de payer ou de recevoir une facture Lightning, mais que vous avez des fonds onchain, vous pouvez utiliser l'adresse onchain que Phoenix vous affiche.

Après la transaction, Phoenix ressemble à ceci :

![img](https://officinebitcoin.it/lezioni/canale/12.webp)

L'app vous avertit que vous devez attendre 3 confirmations de blockchain avant de pouvoir utiliser les fonds.

# Gestion de la liquidité du canal
Dès que vous recevez les 3 confirmations, votre wallet LN est prêt à être utilisé.

Au départ, toute sa liquidité est sortante et vous pouvez seulement dépenser ; vous pouvez le voir dans `Settings -> Advanced -> Payment Channels`

![img](https://officinebitcoin.it/lezioni/canale/13.webp)

Vous pouvez créer de la liquidité entrante en payant une ou plusieurs factures Lightning Network.

# Utilisation du wallet

Utiliser Phoenix wallet est une expérience agréable et très simple.

Les seules choses à garder à l'esprit sont :
1. le canal que vous venez de créer est un smart contract entre vous et Acinq, financé avec vos fonds ;
2. le gros travail de backup des états du canal et de maintenance de son infrastructure est géré par Acinq, qui vous facturera quelques sat supplémentaires en frais pour les opérations de paiement que vous effectuez ;
3. accédez régulièrement à votre wallet, en l'ouvrant et en faisant des opérations de temps en temps car, si la contrepartie remarque votre absence et vous considère comme un "zombie", elle pourrait décider de fermer le canal. Acinq ferme des canaux pour éviter de dépenser des ressources et du temps à maintenir des backups et des canaux dormants ;
4. vous pouvez aussi décider de fermer ce canal si vous n'avez plus besoin de l'utiliser.
5. en cas de fermeture du canal, la procédure de `cooperative closure` est la meilleure, car elle évite de nombreux problèmes.

## Splicing
Une mention spéciale revient à la technique de `Splicing`, mise en œuvre par Acinq et qui permet d'augmenter ou de réduire la capacité totale du canal.

Splicing est intéressant : si vous avez un canal avec une capacité `tot`, vous pouvez l'augmenter ou la réduire. On pourrait penser que ces opérations dépendent des besoins de chacun, **mais ce n'est pas si simple**.

Vous devez toujours garder à l'esprit que **Phoenix est un wallet Lightning Network** et, même s'il prend en charge le Layer1 de Bitcoin, il devrait être utilisé pour de petits paiements sur Layer2.

**Toute opération onchain sera en effet interprétée par Acinq comme une raison de modifier la capacité du canal** :
- recevoir un montant de `xsats` sur Phoenix depuis un wallet onchain : Acinq augmente le canal, portant la capacité de `tot` à `tot + xsats`
- payer un montant de `ysats` depuis Phoenix vers une adresse onchain : Acinq réduit le canal, portant la capacité de `tot` à `tot - ysats`.

`Splicing` est une transaction onchain (multisig 2-de-2) qui entraîne des frais. Même s'ils sont inférieurs à ceux d'une ouverture/fermeture de canal, effectuer ces opérations sans précaution ou au mauvais moment pourrait entraîner des coûts inutilement élevés.

Pour passer de LN à Onchain et inversement, essayez d'utiliser des outils de `swap` appropriés et n'utilisez pas Phoenix Wallet pour cela.

# Récupération des fonds
Enfin, et c'est le plus important, c'est ici que l'importance de disposer d'outils **non-custodial** entre en jeu.

Si et quand le canal est fermé, vous pouvez récupérer vos fonds onchain **en important les 12 mots de backup dans un wallet qui prend en charge le standard BIP39**.

Electrum wallet, entre autres, est une option qui rend cette opération simple et intuitive.

Si le wallet est au contraire *custodial* et que vous ne possédez pas les clés, vous pourriez rencontrer des problèmes, allant de difficultés à interagir avec un *service client impersonnel*, en passant par un lourd `kyc` pour les récupérer, **jusqu'à l'impossibilité de récupérer vos fonds (quel que soit le montant total)**.

Est-ce que cela en vaut la peine ?

# Support d'étude
Si vous avez assisté à la présentation en direct sur Telegram, vous pouvez la considérer comme une étape supplémentaire vers votre souveraineté personnelle (pas seulement financière).
Si vous l'avez manquée, **ne désespérez pas** : ces notes servent précisément à rattraper le contenu et, de plus, sachez que nous la proposerons à nouveau chez Officine.

Pour ne pas manquer la prochaine présentation, rejoignez le [groupe Telegram](https://t.me/officinebitcoin) afin de rester constamment informé.

![img](https://officinebitcoin.it/lezioni/canale/14.webp)

Vous pouvez aussi trouver le [Satoshi Spritz](https://satoshispritz.it/) le plus proche de vous. Un Satoshi Spritz est un meetup local où l'on parle uniquement de Bitcoin, où vous pouvez apporter vos questions et obtenir des réponses d'autres bitcoiners expérimentés. Sur le lien, vous trouverez la carte de la péninsule.

![img](https://officinebitcoin.it/lezioni/canale/15.webp)

Enfin, si vous ne trouvez pas de meetup près de chez vous, vous pouvez profiter des directs hebdomadaires de [SatoshiSpritz Connect](https://t.me/SatoshiSpritzConnect), un meetup virtuel créé pour ceux qui ne peuvent pas participer à Satoshi Spritz, ou pour aider les plus petits meetups à prendre des notes et à trouver de l'inspiration pour leurs propres présentations.

![img](https://officinebitcoin.it/lezioni/canale/16.webp)
