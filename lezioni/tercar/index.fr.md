---
layout: default
title: "Le terminal en mode caractère"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Leçon Bitcoin-only</span> <span>Ce projet est maintenu par valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Le terminal en mode caractère

## Introduction
Linux, ou plus précisément un système GNU Linux, puisque Linux n'est que le kernel qui initialise le matériel et fournit les primitives permettant de l'utiliser, emploie le concept de fichier pour une très grande variété d'activités. Les fichiers sont des séquences de données sur un disque dur, des configurations et pas seulement cela : il existe des filesystems spécifiques qui créent des fichiers d'information permettant de contrôler le fonctionnement de notre ordinateur, et de nombreux dispositifs peuvent aussi être utilisés comme des fichiers, comme des dispositifs de caractères qui traitent de différentes manières des séquences d'octets.

Le processus de chargement du système aboutit à une interface graphique ou, dans notre cas, à un prompt de shell, c'est-à-dire l'interface en mode caractère que nous utiliserons dans nos leçons.

Connaître l'interface permet d'effectuer de nombreuses opérations sur la plupart des dispositifs Linux ; dans notre cours nous considérerons `bash` (bourne again shell), la shell la plus répandue pour Linux. Après le login, nous nous trouverons dans le répertoire home de notre ordinateur, c'est-à-dire dans `\home\pippo` en supposant que notre nom d'utilisateur soit pippo, ou dans `\root` si nous sommes entrés avec le compte superutilisateur (root, justement).

N'UTILISEZ JAMAIS le compte root comme il est d'usage dans d'autres systèmes d'exploitation.

Pour se déplacer entre les répertoires, on peut utiliser la commande `cd` (change directory), en se rappelant qu'elle accepte aussi bien des chemins absolus commençant par `/` que des chemins relatifs depuis le répertoire courant (indiqué par `.` ou sans aucune indication) ou depuis d'autres répertoires comme home (`~`). Si l'on veut obtenir la liste de tous les fichiers présents dans le dossier, on peut utiliser la commande `ls` (list), éventuellement avec l'argument ll, c'est-à-dire `ls -ll`.

## Quelques commandes utiles

Quelques commandes utiles :

- `echo` affiche à l'écran le contenu d'une chaîne passée comme argument,
- `man` appelle le manuel d'une certaine commande,
- `mc` gestionnaire de fichiers en console,
- `nano` éditeur de texte minimal,
- `rm` supprime un fichier,
- `mkdir` crée un répertoire,
- `rmdir` supprime un répertoire (qui doit être vide),
- `touch` crée un fichier vide ou modifie la date d'un fichier existant,
- `cat` affiche à l'écran le contenu d'un fichier texte,
- `ncdu` permet de parcourir le filesystem ordonné par la taille des fichiers et des répertoires,
- `wget` permet de télécharger un fichier depuis le web,
- `dd` permet de transférer des informations entre fichiers, dispositifs, ...
- `tail` affiche à l'écran les dernières lignes d'un fichier (utile pour les logs avec l'option `-f` (follow))
- `chmod` modifie les propriétés d'un fichier (par exemple, l'argument `+x` permet l'exécution d'un fichier)

Les exécutables présents dans le dossier courant peuvent être exécutés en préfixant `./`, c'est-à-dire en indiquant que le chemin se réfère au répertoire courant.

## Redirection d'input/output
La redirection d'input et d'output peut se faire avec les symboles `<` et `>`.

Pour écrire dans un fichier, nous pouvons exécuter

```
echo "pippo" > pippo.txt
```

Cela créera un fichier nommé pippo.txt avec le contenu pippo ; si ensuite nous tapons

```
echo "pluto" > pippo.txt
```

Le contenu du fichier sera remplacé par pluto. Si nous voulions conserver le contenu précédent et ajouter le nouveau contenu à la fin, nous devons utiliser `>>` au lieu de `>`.

Le symbole `<` fonctionne de manière similaire pour les inputs.

## Pipe
Le pipe `|` permet de concaténer l'output d'un programme avec l'input d'un autre.

```
cowsay "good evening" | lolcat
```

L'output de cowsay est transmis à la commande lolcat.

## Variables
Les variables sont des noms donnés à des espaces mémoire qui peuvent contenir des chaînes, des nombres et davantage.

Pour définir une variable, on utilise la commande `=` ; pour l'utiliser, il suffit de préfixer le caractère `$`. Par convention, les variables sont écrites en majuscules.

```
VARIABLE="pippo"
echo $VARIABLE > pippo.txt
VARIABLE="pluto"
echo $VARIABLE >> pippo.txt
```

Crée un fichier avec le contenu

```
pippo
pluto
```

On peut aussi lancer un programme et enregistrer l'output dans une variable

```
VARIABLE=$(ls)
```

L'output de la commande ls est enregistré dans la variable nommée VARIABLE.

## Scripts
Les scripts sont des listes de commandes exécutées en séquence.

La première commande est l'interpréteur utilisé pour lancer la commande, normalement `#!/bin/sh`, c'est-à-dire l'exécutable `/bin/sh` avec le préfixe `#!`.

Avant de les exécuter, ils nécessitent les permissions d'exécution avec la commande `chmod +x filename`.

## Répétitions
Cette leçon est répétitive et sera répétée chaque semaine. Ci-dessous se trouve la liste des répétitions déjà tenues.

| Date        | Notes                                          |
|-------------|------------------------------------------------|
| 240122-2230 | Première leçon                                 |
| 240129-2230 | Bash script                                    |
| 240205-2230 | Bash script                                    |
