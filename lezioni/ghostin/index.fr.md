---
layout: default
title: "Ghostinbox.it: utiliser l email sans posséder d email"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Leçon Bitcoin-only</span> <span>Ce projet est maintenu par valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Ghostinbox.it: utiliser l email sans posséder d email

Ghostinbox est une plateforme web qui permet aux utilisateurs de créer des adresses email temporaires afin de recevoir des messages sans révéler leur véritable adresse email. Le service est idéal pour les inscriptions rapides, les vérifications de compte, les tests de délivrabilité email ou toute situation dans laquelle on souhaite éviter le spam ou protéger son identité.

Contrairement aux services email traditionnels, Ghostinbox ne demande pas d'inscription et ne stocke pas de données personnelles, ce qui en fait un excellent choix pour les personnes qui privilégient la confidentialité. De plus, la prise en charge du réseau Tor permet un accès anonyme au service en masquant l'adresse IP de l'utilisateur. La nature open-source du projet garantit la transparence et permet aux développeurs d'examiner le code à la recherche de vulnérabilités potentielles ou de possibilités de personnalisation.

## Comment fonctionne Ghostinbox ?
![alt text](https://officinebitcoin.it/lezioni/ghostin/front.png)

L'utilisation de Ghostinbox est extrêmement intuitive et ne nécessite aucune compétence technique :

1. **Accéder au site** : Visitez https://ghostinbox.it/ (ou passez par Tor pour davantage d'anonymat).
2. **Générer une adresse email temporaire** : Cliquez sur le bouton pour créer une nouvelle adresse email temporaire (par exemple, random@ghostinbox.it). L'adresse est immédiatement active et prête à l'emploi.
3. **Recevoir des messages** : Utilisez l'adresse générée pour recevoir des emails, par exemple pour des inscriptions à des services en ligne, des vérifications de compte ou des tests. Les messages apparaissent en temps réel dans la boîte de réception sur le site.
4. **Surveiller les messages** : Accédez à la boîte de réception temporaire directement sur Ghostinbox pour consulter les messages reçus. Aucun client email externe n'est nécessaire.

![alt text](https://officinebitcoin.it/lezioni/ghostin/email.png)

Le service est conçu pour être rapide et sans friction : aucune création de compte n'est nécessaire, et l'interface minimaliste rend l'expérience fluide même pour les utilisateurs non techniques. La possibilité d'accès via Tor ajoute un niveau de protection supplémentaire pour les personnes qui souhaitent conserver un anonymat complet.

## De l'alias à l'email
Pour utiliser le service, il faut choisir un alias suffisamment long et aléatoire pour qu'il ne puisse pas être deviné par d'autres utilisateurs. Cet alias servira comme un mot de passe pour accéder à l'email et ne doit donc pas être oublié.

À partir de cet alias, une adresse email HASH@ghostinbox.it est dérivée, où HASH correspond à `sha256(alias)`, c'est-à-dire au hash de l'alias avec SHA-256 ; l'utilisateur peut ensuite utiliser cet email (affiché dans le schéma de réception) pour recevoir des emails. La page de réception se met à jour automatiquement en affichant les emails reçus. Un utilisateur peut créer une adresse email sans accéder au service et utiliser le site uniquement pour la consultation.

En cliquant sur l'email, on peut lire son texte et éventuellement copier des liens à ouvrir ; le format de l'email est volontairement en texte seul et n'affichera donc aucun des éléments graphiques des emails basés sur HTML.

## Qui a besoin de Ghostinbox ?
Ghostinbox répond à différents besoins liés à la confidentialité et à la gestion d'emails temporaires :

1. **Protection contre le spam** : En utilisant une adresse temporaire, les utilisateurs peuvent éviter que leur véritable adresse email soit submergée de spam ou de newsletters indésirables.
2. **Inscriptions sécurisées** : Parfait pour s'inscrire à des services en ligne, des forums ou des plateformes qui exigent une vérification par email sans compromettre l'email personnel.
3. **Tests de délivrabilité** : Les développeurs et les spécialistes marketing peuvent utiliser Ghostinbox pour tester l'envoi et la réception d'emails sans impliquer de véritables adresses.
4. **Confidentialité avancée** : Grâce à la prise en charge de Tor, le service est idéal pour les utilisateurs qui souhaitent rester anonymes lorsqu'ils interagissent avec des sites web ou des services en ligne.
5. **Usage temporaire** : Adapté aux situations où une adresse email jetable est nécessaire, comme les promotions, les essais gratuits ou les communications de courte durée.

![alt text](https://officinebitcoin.it/lezioni/ghostin/stats.png)

## Caractéristiques techniques
Le dépôt GitHub de Ghostinbox (https://github.com/valerio-vaccaro/ghostinbox.it) révèle une implémentation légère, écrite principalement en Python avec le framework Flask, avec les caractéristiques suivantes :

- **Approche serverless** : il n'y a pas de serveur email ; le service exploite plutôt un service gratuit d'email et de transfert d'email, ce qui rend son architecture extrêmement simple et économique.
- **Architecture** : Ghostinbox utilise une architecture client-serveur basée sur Flask pour gérer la génération des adresses email temporaires et l'affichage des messages. La simplicité de la conception garantit de hautes performances même avec de grands volumes de requêtes.
- **Génération des adresses** : Les adresses email temporaires sont générées dynamiquement à partir de l'alias saisi.
- **Support Tor** : Le service est configuré pour être accessible via onion routing, ce qui garantit que l'adresse IP de l'utilisateur n'est pas suivie pendant l'interaction avec le site.
- **Gestion des messages** : Les messages reçus sont supprimés après 30 jours.
- **Sécurité** : Aucune donnée personnelle ni aucun message n'est stocké de façon permanente. La conception du service minimise les risques de brèche, et l'absence d'inscription supprime la nécessité de fournir des informations sensibles.
- **Open-source** : Le code public permet aux développeurs de vérifier l'intégrité du système, de contribuer des améliorations ou d'héberger une instance personnalisée.

Points forts techniques :
- **Confidentialité absolue** : La suppression des emails après 30 jours et le support Tor garantissent une expérience anonyme et sûre.
- **Légèreté** : L'implémentation Flask est optimisée pour de faibles ressources, ce qui rend le service évolutif et rapide.
- **Transparence** : La licence open-source permet l'audit du code et les personnalisations, renforçant la confiance des utilisateurs.

## Conclusion
Ghostinbox est une solution élégante et fonctionnelle pour les personnes qui recherchent un service d'email temporaire rapide, sûr et orienté vers la confidentialité. Avec son interface intuitive, le support Tor et la transparence de son code open-source, il s'adresse aussi bien aux utilisateurs ordinaires qui veulent protéger leur boîte de réception du spam qu'aux développeurs qui ont besoin d'un système fiable pour des tests ou des inscriptions temporaires. Pour essayer Ghostinbox, visitez https://ghostinbox.it/. Pour explorer le code ou contribuer au projet, consultez le dépôt à l'adresse https://github.com/valerio-vaccaro/ghostinbox.it.

