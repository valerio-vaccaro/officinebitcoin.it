---
layout: default
title: "Tutoriel GPG et YubiKey"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Leçon Bitcoin-only</span> <span>Ce projet est maintenu par valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Tutoriel GPG et YubiKey

Cette leçon vous guide dans l'utilisation de Gnu Privacy Guard (GPG) :
- pour créer une nouvelle paire de clés,
- ajouter des sous-clés pour la signature et le chiffrement,
- sauvegarder toutes les clés,
- transférer des sous-clés vers une YubiKey, et
- chiffrer/signer un fichier avec Yubikey.

Elle est conçue pour Linux, avec des commandes testées sur GPG 2.2.40/Debian 12. Les mêmes commandes peuvent fonctionner de façon similaire sur d'autres versions de Linux ainsi que sur MacOSX et Windows (sauf pour les systèmes de fichiers chiffrés).

Le processus suit les bonnes pratiques de sécurité, comme la génération de clés hors ligne et les sauvegardes sécurisées.

## Installation
Installez gpg et les utilitaires nécessaires

```bash
sudo apt update
sudo apt install gnupg scdaemon pcscd yubikey-manager
```

Assurez-vous que la version est 2.1.17 ou ultérieure (2.4.5 recommandée).

```bash
gpg --version
```

Vérifiez le fonctionnement de la YubiKey

```bash
ykman info
```

Assurez-vous que l'applet OpenPGP est activé et que le mode CCID est actif.

Utilisez une machine isolée du réseau (sans internet) pour générer les clés et éviter les fuites.

N'oubliez pas que les PIN par défaut de YubiKey ne sont pas sûrs et sont :
- Default User PIN: 123456
- Default Admin PIN: 12345678
Changez-les avant utilisation (voir l'étape 4).

## Étape 1
Générez une paire de clés GPG primaire (publique et privée) uniquement pour la certification (C) ; toutes les autres clés en dériveront.

Démarrez la génération de clés avec --expert pour accéder aux options avancées.

```bash
gpg --expert --full-gen-key
```

Sélectionnez le type de clé :

```
Please select what kind of key you want:
   (1) RSA and RSA (default)
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
   (7) DSA (set your own capabilities)
   (8) RSA (set your own capabilities)
   (9) ECC and ECC
  (10) ECC (sign only)
  (11) ECC (set your own capabilities)
  (13) Existing key
  (14) Existing key from card
Your selection? 8
```

Choisissez (8) RSA (set your own capabilities) pour personnaliser le comportement de la clé.

Configurez les capacités :

```
Possible actions for a RSA key: Sign Certify Encrypt Authenticate 
Current allowed actions: Sign Certify Encrypt 

   (S) Toggle the sign capability
   (E) Toggle the encrypt capability
   (A) Toggle the authenticate capability
   (Q) Finished

Your selection? S
```

Désactivez Sign et Encrypt (appuyez sur S, E).

Conservez Certify (appuyez sur Q une fois terminé).

Ainsi, seul Certify reste parmi les actions autorisées.

Définissez la taille de la clé :

```
RSA keys may be between 1024 and 4096 bits long.
What keysize do you want? (3072) 4096
```

Saisissez 4096 (maximum pris en charge par YubiKey 4/5).

Définissez l'expiration :

```
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0) 
```

Saisissez 3y (3 ans) ou votre préférence. Confirmez la date.

Saisissez l'User ID :

```
GnuPG needs to construct a user ID to identify your key.

Real name: Satoshi Spritz
Email address: info@satoshispritz.it
Comment: 
You selected this USER-ID:
    "Satoshi Spritz <info@satoshispritz.it>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? o
```

Indiquez le nom et l'e-mail. Laissez le commentaire vide. Confirmez avec O.

Saisissez une passphrase forte (mélangez lettres, chiffres et symboles ; évitez les mots courants).

Exemple : Tr0ub4dor&3xplor3r!2025

La passphrase protège votre clé privée.

Générez de l'entropie en déplaçant la souris, en tapant au hasard ou en utilisant rng-tools (Linux et seulement si vous comprenez bien son fonctionnement) :

```bash
sudo apt install rng-tools
sudo rngd -r /dev/urandom
```

Attendez la fin de la génération de la clé. Notez le key ID (par exemple C2033656849FC82BA3C365E33C9BF8B9CB86875D) dans la sortie :

```
gpublic and secret key created and signed.

pub   rsa2048 2025-07-20 [C]
      C2033656849FC82BA3C365E33C9BF8B9CB86875D
uid                      Satoshi Spritz <info@satoshispritz.it>

```

Créez un certificat de révocation au cas où la clé serait compromise (votre client l'a peut-être déjà créé) :

```bash
gpg --output revoke_master_satoshispritz.asc --gen-revoke C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Choisissez le motif (par exemple 1 = clé compromise) et enregistrez.

## Étape 2
Créez des sous-clés de signature et de chiffrement. Deux sous-clés seront ajoutées pour la signature (S) et le chiffrement (E).

La clé primaire reste réservée à la certification.

Modifiez la clé :

```bash
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Saisissez la passphrase si elle est demandée.

Ajoutez la sous-clé de signature :

```
gpg> addkey
Please select what kind of key you want:
   (3) DSA (sign only)
   (4) RSA (sign only)
   (5) Elgamal (encrypt only)
   (6) RSA (encrypt only)
   (7) DSA (set your own capabilities)
   (8) RSA (set your own capabilities)
  (10) ECC (sign only)
  (11) ECC (set your own capabilities)
  (12) ECC (encrypt only)
  (13) Existing key
  (14) Existing key from card
Your selection? 4
```

Choisissez (4) RSA (sign only).

Définissez la taille : 4096.

Définissez l'expiration : 2y (2 ans, les sous-clés peuvent être renouvelées plus fréquemment).

Confirmez et saisissez la passphrase.

Ajoutez la sous-clé de chiffrement :

```
gpg> addkey
```

Choisissez (6) RSA (encrypt only).

Définissez la taille : 4096.

Définissez l'expiration : 2y.

Confirmez et saisissez la passphrase.

Enregistrez les modifications :

```
gpg> save
```

Vérifiez les sous-clés :

```bash
gpg --list-keys --with-subkey-fingerprints C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Exemple de sortie :

```
pub   rsa4096 2025-07-20 [C] [expires: 2028-07-20]
      C2033656849FC82BA3C365E33C9BF8B9CB86875D
uid           [ultimate] Satoshi Spritz <info@satoshispritz.it>
sub   rsa4096 2025-07-20 [S] [expires: 2027-07-20]
      1E3C548D2CA2927D205C1A85426E4AB8E6D72AC3
sub   rsa4096 2025-07-20 [E] [expires: 2027-07-20]
      94C11C615BE049B97899FA3C8DC3736F499D6C3E

```

Notez les fingerprints des sous-clés de signature (S) et de chiffrement (E).

## Étape 3
Sauvegarde de toutes les clés. Sauvegardez la clé primaire, les sous-clés et la clé publique sur deux clés USB chiffrées par sécurité.

Préparez les clés USB : insérez deux clés USB (par exemple /dev/sdb et /dev/sdc).

Créez des partitions chiffrées (par exemple avec LUKS) :

```bash
sudo cryptsetup luksFormat /dev/sdb1
sudo cryptsetup luksOpen /dev/sdb1 backup1
sudo mkfs.ext4 /dev/mapper/backup1
sudo mount /dev/mapper/backup1 /mnt/backup1
```

Répétez pour /dev/sdc1 (par exemple montée sur /mnt/backup2).

Exportez les clés privées : exportez la clé primaire et les sous-clés :

```bash
gpg --armor --export-secret-keys C2033656849FC82BA3C365E33C9BF8B9CB86875D! > /mnt/backup1/secret_master_satoshispritz.asc
gpg --armor --export-secret-keys 1E3C548D2CA2927D205C1A85426E4AB8E6D72AC3! > /mnt/backup2/secret_sign_satoshispritz.asc
gpg --armor --export-secret-keys 94C11C615BE049B97899FA3C8DC3736F499D6C3E! > /mnt/backup2/secret_encrypt_satoshispritz.asc
```

Exportez les clés publiques :

```bash
gpg --armor --export C2033656849FC82BA3C365E33C9BF8B9CB86875D! > /mnt/backup1/public_master_satoshispritz.asc
gpg --armor --export 1E3C548D2CA2927D205C1A85426E4AB8E6D72AC3! > /mnt/backup2/public_sign_satoshispritz.asc
gpg --armor --export 94C11C615BE049B97899FA3C8DC3736F499D6C3E! > /mnt/backup2/public_encrypt_satoshispritz.asc
```

Exportez le certificat de révocation :

```bash
cp revoke_master_satoshispritz.asc /mnt/backup1/revoke_master_satoshispritz.asc
cp revoke_master_satoshispritz.asc /mnt/backup2/revoke_master_satoshispritz.asc
```

Démontez en toute sécurité :

```bash
sudo umount /mnt/backup1
sudo cryptsetup luksClose backup1
```

Répétez pour backup2. Stockez les clés USB dans des lieux séparés et sûrs (par exemple un coffre).

Supprimez les clés locales (facultatif) : si vous utilisez une machine isolée du réseau, supprimez le répertoire GPG :

```bash
rm -rf ~/.gnupg
```

Les clés devront ensuite être importées sur la machine où vous les utiliserez.

Si la machine n'est pas isolée du réseau, conservez les clés jusqu'au transfert vers la YubiKey.

## Étape 4
Transférez les sous-clés de signature et de chiffrement vers la YubiKey, en gardant la clé primaire hors ligne.

Insérez la Yubikey et vérifiez :

```bash
gpg --card-status
```

La sortie doit afficher l'applet OpenPGP (par exemple Version: 2.0).

Changez les PIN par défaut :

```bash
gpg --change-pin
```

User PIN : définissez un nouveau PIN de 6 à 8 chiffres (par exemple 654321).
Admin PIN : définissez un nouveau PIN de 8 chiffres (par exemple 87654321).

Modifiez la clé pour le transfert :

```bash
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Sélectionnez et transférez la sous-clé de signature : listez les clés pour identifier les indices des sous-clés :

```
gpg> list
```

Exemple :

```
sec  rsa4096/3C9BF8B9CB86875D
     created: 2025-07-20  expires: 2028-07-20  usage: C   
     trust: ultimate      validity: ultimate
ssb  rsa4096/426E4AB8E6D72AC3
     created: 2025-07-20  expires: 2027-07-20  usage: S   
ssb  rsa4096/8DC3736F499D6C3E
     created: 2025-07-20  expires: 2027-07-20  usage: E
```

Sélectionnez la sous-clé de signature :

```
gpg> key 1
```

La sous-clé de signature aura un astérisque (*).

Transférez vers la YubiKey :

```
gpg> keytocard
Please select where to store the key:
   (1) Signature key
   (3) Authentication key
Your selection?
```

Saisissez l'Admin PIN (par exemple 87654321). La sous-clé privée de signature est transférée vers la YubiKey et remplacée par un stub dans le keyring.

Sélectionnez et transférez la sous-clé de chiffrement : désélectionnez la sous-clé de signature :

```
gpg> key 1
```

Sélectionnez la sous-clé de chiffrement :

```
gpg> key 2
```

Transférez vers la YubiKey :

```
gpg> keytocard
Please select where to store the key:
   (2) Encryption key
Your selection? 2
```

Saisissez de nouveau l'Admin PIN.

Enregistrez les modifications :

```
gpg> save
```

Les sous-clés privées sont maintenant sur la YubiKey, avec des stubs locaux.

Vérifiez la YubiKey :

```bash
gpg --card-status
```

Vérifiez que les emplacements Signature key et Encryption key affichent les fingerprints des sous-clés.

Exportez les sous-clés privées (pour vérifier la sauvegarde) :

```bash
gpg --armor --export-secret-subkeys C2033656849FC82BA3C365E33C9BF8B9CB86875D > secret-subkeys-satoshispritz.asc
```

Supprimez le répertoire GPG local :

```bash
rm -rf ~/.gnupg
```

Réimportez la clé publique et les stubs :

```bash
gpg --import public.asc
gpg --import secret-subkeys-satoshispritz.asc
```

La clé privée primaire n'est plus sur l'ordinateur.

## Étape 5
Utilisez la YubiKey pour chiffrer et signer un fichier destiné à un destinataire.

Préparez un fichier de test :

```bash
echo "This is a secret message." > test.txt
```

Obtenez la clé publique du destinataire (par exemple bob@example.com) :

```bash
gpg --keyserver hkps://keys.openpgp.org --search-keys bob@example.com
```

Ou importez-la depuis un fichier :

```bash
gpg --import bob_public.asc
```

Chiffrez et signez : chiffrez pour bob@example.com et signez avec Yubikey :

```bash
gpg --encrypt --sign --recipient bob@example.com test.txt
```

Saisissez l'User PIN (par exemple 654321) lorsque demandé.

Si YubiKey exige une confirmation tactile (facultatif, configurée via ykman openpgp keys set-touch), touchez la YubiKey.

La sortie sera test.txt.gpg

Déchiffrez le fichier (nécessite YubiKey) :

```bash
gpg --decrypt test.txt.gpg > test_decrypted.txt
```

Saisissez l'User PIN et touchez la Yubikey si nécessaire.

Vérifiez que test_decrypted.txt correspond à test.txt.

Bob peut déchiffrer avec sa clé privée et vérifier votre signature :

```bash
gpg --decrypt test.txt.gpg
```

Si vous voulez seulement signer le fichier, vous pouvez utiliser les commandes suivantes.

```bash
gpg --detach-sign test.txt
```

Cela générera un fichier de sortie nommé test.txt.sig

Pour le vérifier :

```bash
gpg --verify test.txt.sig test.txt
```

## Pratiques de sécurité
- Générez toujours les clés sur une machine hors ligne afin d'éviter l'exposition.
- Stockez les clés USB contenant des clés privées dans des lieux séparés et sûrs (par exemple coffre ou banque).
- Utilisez des PIN forts et uniques. Si les tentatives de PIN sont dépassées (3 pour User, 3 pour Admin), la Yubikey se bloque et nécessite une réinitialisation, ce qui fait perdre toutes les clés.
- Gardez revoke.asc accessible mais sécurisé pour révoquer la clé si elle est compromise.
- Créez de nouvelles sous-clés avant l'expiration (par exemple chaque année) comme suit :

```bash
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
gpg> addkey
```

Transférez les nouvelles sous-clés vers la YubiKey et mettez à jour la clé publique sur les serveurs :

```bash
gpg --keyserver hkps://keys.openpgp.org --send-keys C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Utilisez une seconde YubiKey pour la redondance :

```bash
gpg --import secret.asc
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Répétez les étapes keytocard pour la seconde YubiKey.

Si vous devez réinitialiser la Yubikey :

```bash
ykman openpgp reset
```

Pour restaurer les sous-clés depuis la sauvegarde :

```bash
gpg --import secret.asc
```

“Public Key Not Usable” : assurez-vous que la clé publique du destinataire est importée et considérée comme fiable :

```bash
gpg --edit-key bob@example.com
gpg> trust
```
Définissez sur 5 = Ultimate trust.
