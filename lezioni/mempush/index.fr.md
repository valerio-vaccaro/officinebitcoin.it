---
layout: default
title: "MemPush : envoyer et gérer des transactions Bitcoin dans la mempool en toute simplicité"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Leçon Bitcoin-only</span> <span>Ce projet est maintenu par valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# MemPush : envoyer et gérer des transactions Bitcoin dans la mempool en toute simplicité

MemPush (https://mempush.com/) est une plateforme innovante qui rend l'envoi et la gestion des transactions Bitcoin dans la mempool simples, sûrs et accessibles. La mempool, le "réservoir" temporaire des transactions Bitcoin en attente de confirmation sur la blockchain, est au coeur de ce service, qui élimine les complexités techniques pour les utilisateurs et les développeurs.

## Qu'est-ce que MemPush ?

MemPush est un service web qui permet d'envoyer des raw Bitcoin transactions (au format hexadécimal) directement vers la mempool, sans configuration avancée ni Bitcoin nodes personnels. Conçu par Valerio Vaccaro, MemPush prend aussi en charge le réseau Tor afin de garantir une meilleure confidentialité aux utilisateurs.

![alt text](https://officinebitcoin.it/lezioni/mempush/front.png)

Le code source, disponible sur GitHub (https://github.com/valerio-vaccaro/mempush) sous licence open-source, permet à chacun de vérifier la sécurité du projet, de contribuer à son développement ou d'héberger une instance personnalisée du service.

## Comment fonctionne MemPush ?

L'interface de MemPush est intuitive et facile à utiliser :

1. **Accéder au site** : visitez https://mempush.com/.
2. **Saisir la raw transaction** : collez la transaction Bitcoin au format hexadécimal dans le champ dédié.
3. **Envoyer la transaction** : cliquez sur "Submit Raw Transaction" pour propager la transaction vers la mempool à travers des Bitcoin nodes.
4. **Suivre le statut** : vérifiez l'avancement de la transaction avec un blockchain explorer.
5. **Retransmission automatique** : MemPush retransmet automatiquement les transactions, si nécessaire, afin d'assurer leur maintien dans la mempool.

![alt text](https://officinebitcoin.it/lezioni/mempush/list.png)

Aucune inscription n'est requise, et l'approche open-source élimine les risques cachés, ce qui rend MemPush idéal même pour les utilisateurs moins expérimentés.

## À qui s'adresse MemPush ?

MemPush est conçu pour répondre à différents besoins :
1. **Frais faibles** : les transactions avec des frais faibles sont automatiquement retransmises afin d'éviter leur retrait de la mempool lors des pics de trafic.
2. **Transactions timelocked** : prend en charge la surveillance et la retransmission des transactions soumises à des contraintes temporelles, en garantissant leur gestion effective.
3. **Surveillance avancée** : MemPush vérifie périodiquement le statut des transactions, en permettant de retirer uniquement les transactions confirmées ou invalidées (par exemple, les double-spends).
4. **Confidentialité renforcée** : grâce à la prise en charge du réseau Tor, MemPush protège l'anonymat de l'utilisateur lors de l'envoi de transactions.

## Caractéristiques techniques

Le dépôt GitHub (https://github.com/valerio-vaccaro/mempush) présente une implémentation Python élégante, basée sur le framework Flask et intégrée à une base de données pour la gestion des transactions. MemPush s'appuie sur des services comme blockstream.info et mempool.space pour surveiller et propager les transactions, avec des projets futurs d'intégration d'un Bitcoin node local.

Principaux points forts :
- **Sécurité** : aucune donnée sensible ni clé privée n'est stockée, ce qui garantit une protection totale.
- **Scalabilité** : prend en charge un volume élevé de transactions grâce à une connexion directe au réseau Bitcoin.
- **Open-source** : le code public permet la vérification, les contributions et les personnalisations par la communauté.

## Conclusion

MemPush est une solution puissante et accessible pour toute personne souhaitant envoyer et gérer des transactions Bitcoin dans la mempool sans complications. Grâce à sa transparence, à son support de la confidentialité et à sa facilité d'utilisation, il représente un ajout précieux à l'écosystème Bitcoin. Visitez https://mempush.com/ pour l'essayer ou explorez le code sur https://github.com/valerio-vaccaro/mempush.
