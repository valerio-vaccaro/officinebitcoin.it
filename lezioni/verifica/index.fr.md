---
layout: default
title: "Prérequis pour ce tutoriel"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Leçon Bitcoin-only</span> <span>Ce projet est maintenu par valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

![cover](https://officinebitcoin.it/lezioni/verifica/1cover.webp)
Vérifier les signatures cryptographiques est une pratique de sécurité fondamentale que **tout utilisateur de logiciel open-source devrait intégrer à sa routine de bonnes habitudes**.

L'open source est par nature modifiable, ce qui signifie que n'importe qui peut, en théorie, introduire des backdoors, des attaques ou du code malveillant dans les applications que vous utilisez pour pratiquer pendant votre apprentissage du protocole Bitcoin.

En tant qu'utilisateur qui approfondit son étude, vous avez la possibilité de vérifier personnellement si le logiciel téléchargé a été altéré, et vous devriez le faire avant de l'installer et de l'utiliser.

Avant de commencer, nous apportons aussi un classique des présentations à Officine Bitcoin : le meme. Ce ne sera pas une présentation lourde, mais détendons l'atmosphère dès le départ.

![meme](https://officinebitcoin.it/lezioni/verifica/2meme.webp)

## Comment faire ?
Les développeurs publient toujours de nouvelles versions de logiciel accompagnées d'une signature cryptographique.
Cela signifie qu'en plus d'avoir mis à jour le logiciel, ils le publient en certifiant l'avoir lié à une fingerprint spécifique. Rappel : la signature numérique produite avec la clé privée est unique et non modifiable.

Il vous suffit de disposer de la suite GPG pour procéder à la vérification de la signature.

![img](https://officinebitcoin.it/lezioni/verifica/3.webp)

# Prérequis pour ce tutoriel
- Une brève révision de la cryptographie asymétrique
- Les éléments à vérifier :
  - software (binary, apk, etc.)
  - la signature numérique du développeur, généralement un fichier `.asc`, `.sig` ou un checksum.
- Les outils de vérification :
  - suite GPG
  - un terminal (fonctionne aussi bien sous Linux que sous Windows)
# Cryptographie asymétrique

![img](https://officinebitcoin.it/lezioni/verifica/4.webp)

Il y a ici deux clés liées entre elles : une clé publique et une clé privée. Comme leurs noms l'indiquent :
- La clé publique est librement disponible et peut être partagée avec n'importe qui.
- La clé privée est conservée en sécurité par son propriétaire.

Les données chiffrées avec la clé publique ne peuvent être déchiffrées que par la clé privée correspondante. Cela permet à quiconque d'envoyer des données chiffrées au propriétaire de la paire de clés, sans partage préalable de la partie secrète.

La cryptographie à clé publique est plus lente que la cryptographie symétrique et ne convient pas au chiffrement de grandes quantités de données. Toutefois, elle permet une distribution sécurisée des clés de chiffrement.
Parmi les algorithmes couramment utilisés pour la cryptographie à clé publique figurent RSA, ECC, ElGamal et DSA.

## Côté développeur : nouvelle mise à jour

Le développeur publie le code open source, qui par nature n'est pas chiffré.
Il crée un hash cryptographique (qui génère le `checksum`) et chiffre le digest avec sa clé privée : cela crée la signature, ce fichier `.sig` ou `.asc` mentionné plus haut.

Après ce processus, le développeur téléverse les deux fichiers sur le site ou dans un dépôt GitHub. C'est là que votre téléchargement commence.

![img](https://officinebitcoin.it/lezioni/verifica/5.webp)

Ensuite, vous aurez besoin de la clé publique du développeur. Parfois elle se trouve dans le dépôt GitHub, parfois sur des serveurs publics (*keyservers*). Même si la recherche peut demander des efforts, la clé publique est un élément essentiel pour vérifier le logiciel, alors faites l'effort de l'obtenir.

Si vous avez des difficultés, posez vos questions dans le groupe Telegram d'Officine Bitcoin, où vous trouverez des instructions pour obtenir une clé publique spécifique.

![img](https://officinebitcoin.it/lezioni/verifica/6.webp)

Pour vérifier l'intégrité des données, le destinataire déchiffre la signature à l'aide de la clé publique de l'expéditeur et obtient un résultat :

a. les données sont considérées comme authentiques et non modifiées pendant le transit.
b. les données ont potentiellement été altérées.

En chiffrant la valeur du hash avec la clé privée, **les signatures PGP garantissent que le checksum lui-même est protégé et lié à l'identité de l'expéditeur. Cela empêche la falsification de signatures sur des données altérées**.

Les signatures peuvent servir à vérifier n'importe quoi : fichiers, emails, documents et téléchargements de logiciels. Lorsque vous vérifiez une signature PGP, vous prouvez que les données proviennent réellement d'une source fiable et qu'elles sont intactes.

Et c'est la vérification d'un apk mobile que vous allez maintenant pouvoir effectuer.

Nous prenons comme exemple le téléchargement de Phoenix, un wallet LN non-custodial, afin de pouvoir l'aborder spécifiquement lors d'une future soirée Officine Bitcoin.

# Télécharger et vérifier Phoenix Wallet (Acinq)
Si vous êtes déjà allé sur le site d'[Acinq](https://phoenix.acinq.co/), le développeur de Phoenix, vous savez déjà que le téléchargement est disponible sur les stores officiels pour Android et iOS.
Vous ne l'avez peut-être jamais remarqué, mais pour Android le fichier apk est aussi disponible.

![img](https://officinebitcoin.it/lezioni/verifica/8.webp)

[Allons-y !](https://github.com/ACINQ/phoenix/releases) pour trouver les fichiers `apk` et `Signature` que vous téléchargerez avec `wget`.
Dans le cas de Phoenix, le fichier contenant la signature pour la vérification s'appelle **`SHA256SUMS.ASC`**.

![img](https://officinebitcoin.it/lezioni/verifica/9.webp)

Dans le même dépôt se trouvent aussi les instructions pour télécharger la clé publique correspondant à la *signing key E04E48E72C205463* (fingerprint unique des clés de Drouinf).
Copiez le lien et téléchargez-le avec `wget`, ou suivez les instructions proposées dans la section appropriée du repo.

![img](https://officinebitcoin.it/lezioni/verifica/10.webp)

---
⚠️**La clé publique doit être importée, pas seulement téléchargée**.
⚠️ Les téléchargements des fichiers doivent se faire dans le même répertoire.

---
# Ouvrir le terminal
Avec le terminal, naviguez jusqu'au répertoire où l'apk et le fichier `SHA256SUMS.ASC` ont été téléchargés, puis exécutez les commandes dans l'ordre.

![img](https://officinebitcoin.it/lezioni/verifica/11.webp)

![img](https://officinebitcoin.it/lezioni/verifica/12.webp)

Lorsque la vérification renvoie un résultat positif, vous pouvez transférer l'apk sur votre téléphone et installer l'app.

---
# Vérification difficile
Il peut y avoir plusieurs raisons pour lesquelles la vérification de signature n'est pas facile, et elles sont presque toujours dues au désordre ou à l'inexpérience :
1. les fichiers apk et/ou .asc ont été téléchargés plusieurs fois, si bien que dans le répertoire ils apparaissent avec, par exemple, des noms étranges comme **filename-1** ou **filename(1)**
2. apk et .asc ne sont pas dans le même répertoire
3. la clé publique a été téléchargée mais pas importée dans le keyring de gpg.

D'autres situations peuvent se présenter où, même en opérant correctement, la vérification échoue.
Il est important de vérifier l'erreur qui apparaît dans le terminal, de la copier et de lancer une recherche sur internet pour trouver la solution.

# Vérification avec Sparrow Wallet
Si vous utilisez déjà Sparrow Wallet, vous pouvez procéder à la vérification des téléchargements avec ce logiciel, **dont le téléchargement et l'installation doivent être précédés d'une vérification attentive et rigoureuse avec GPG**.

Lancez Sparrow wallet et cherchez dans le menu `Tools` -> `Verify Downloads`.

![img](https://officinebitcoin.it/lezioni/verifica/13.webp)

Une interface s'ouvre et vous demande d'insérer les fichiers fraîchement téléchargés. En cliquant sur `Browse`, le gestionnaire de fichiers s'ouvre pour charger chaque fichier dans le champ requis.

![img](https://officinebitcoin.it/lezioni/verifica/14.webp)

Parfois le formulaire de l'interface se remplit tout seul. Si ce n'est pas le cas, remplissez tous les champs avec les fichiers appropriés.

![img](https://officinebitcoin.it/lezioni/verifica/15.webp)

Le résultat positif est affiché graphiquement par des coches vertes et par la confirmation *`Ready to install`* + < filename >.

# Soutien à l'étude
Si vous avez assisté à la présentation en direct sur Telegram, vous pouvez la considérer comme une étape supplémentaire vers votre souveraineté personnelle (pas seulement financière).
Si vous l'avez manquée, **ne désespérez pas** : ces notes servent précisément à rattraper, et de plus, sachez que nous la proposerons de nouveau à Officine.

Pour ne pas manquer la prochaine présentation, rejoignez le [groupe Telegram](https://t.me/officinebitcoin) afin de rester constamment informé.

![img](https://officinebitcoin.it/lezioni/verifica/17.webp)

Vous pouvez aussi trouver le [Satoshi Spritz](https://satoshispritz.it/) le plus proche de chez vous. Un Satoshi Spritz est un meetup local où l'on parle uniquement de Bitcoin, où vous pouvez apporter vos questions et obtenir des réponses d'autres bitcoiners experts. Au lien, vous trouverez la carte de la péninsule.

![img](https://officinebitcoin.it/lezioni/verifica/16.webp)

Enfin, si vous ne trouvez pas de meetup près de chez vous, vous pouvez profiter des directs hebdomadaires de [SatoshiSpritz Connect](https://t.me/SatoshiSpritzConnect), un meetup virtuel créé pour ceux qui ne peuvent pas participer à Satoshi Spritz, ou pour aider les meetups plus petits à prendre des notes et à trouver de l'inspiration pour leurs propres présentations.

![img](https://officinebitcoin.it/lezioni/verifica/18.webp)
